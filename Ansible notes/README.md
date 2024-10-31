# Table of contents
- [Table of contents](#table-of-contents)
- [Ansible architecture](#ansible-architecture)
- [Background research](#background-research)
- [Create a EC2 instance for "controller" node](#create-a-ec2-instance-for-controller-node)
  - [Host files](#host-files)
  - [Running ADHOC](#running-adhoc)
  - [Playbook - install nginx + config](#playbook---install-nginx--config)
- [Use ADHOC to copy to target node](#use-adhoc-to-copy-to-target-node)
- [Use a copy a module](#use-a-copy-a-module)
- [Playbook - provision the APP VM](#playbook---provision-the-app-vm)

# Ansible architecture
![alt text](images/archimage.png)
# Background research

**How Ansible Works:**
Ansible operates by connecting to your nodes (servers, cloud instances, network devices, etc.) via SSH (for Linux/Unix systems) or WinRM (for Windows systems) and executing tasks defined in playbooks. 

It uses an agent-less architecture, meaning you don’t need to install any software on the nodes it manages. 

**Key Concepts in Ansible:**

- Playbook: A YAML file where you define automation tasks and configurations. Playbooks describe a series of steps to bring systems to the desired state.

- Tasks: Individual actions within a playbook, such as installing software, configuring services, or modifying files.

- Inventory: A file or dynamic source where you define the hosts or nodes that Ansible will manage. The inventory can be static (a list of servers) or dynamic (generated from a cloud provider).

- Modules: Reusable units of code that perform actions such as installing software, managing files, or interacting with cloud providers. Ansible comes with many built-in modules for various tasks (e.g., managing users, services, and databases).

- Roles: A collection of tasks, files, variables, and handlers organized for reuse across different playbooks or projects.

- Handlers: Tasks that only run when notified by other tasks, usually to restart services after a configuration change.

- Facts: Information gathered about the target system (e.g., IP addresses, OS version) that can be used to make decisions in playbooks.

# Create a EC2 instance for "controller" node
1. create the EC2  instance for our controller vm (make sure it is the correct vm)
2. name it "tech264-anjy-ubuntu-2204-ansible-controller"
3. ssh into the vm
4. do a package update ``sudo apt update``
5. do a package upgrade``sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y``
6. install ansible 
   1. we need out package manager to get the ansible repo ```sudo apt-add-repository ppa:ansible/ansible```
   2. run the package update again (good practice to get the most updated version) ```sudo apt update -y```
   3. next we install ```sudo apt install ansible -y```
   4. check the version ``ansible --version``
   5. it tells you information - including the path to the config file 
   ![alt text](images/ansibleversionimage.png)
   6. cd into the ansible folder ``` cd /etc/ansible``` - useful to get to config files later
7. we need the PRIVATE aws key on the controller node
   1. go to home direc on your vm bash window
   2. cd into .ssh folder 
   3. open a new bash window 
   4. cd into the .ssh folder in your local machine - private key is .pem
   5. cat to display your .pem file and copy the EXACT contents 
   6. in your bash window for your controller vm 
   7. nano and create a file with the SAME name and paste the contents 
   8. remember to save and exit the file "ctrl + s" and "ctrl + x"
   9. check the key is there, for security only the first line ```head -1 "name of key"```
8.  our private key is now on our vm, we need to add permissions
    1.  on the aws page for the ec2 instance - you can see the command to make sure your ley is not publicly visible (400- only the owner can read)
    ![alt text](images/400image-1.png)
    2.  run the chmod command ```chmod 400 "tech264-anjy-aws-key.pem"```
    3.  confirm the permission have changed with ```ls -l``
   ![alt text](images/pemsimage.png)

## Host files
9.  using the ping module- check your controller module can communicate to all the devices in your host file ```ansible all -m ping ```
![alt text](images/pingimage-2.png)
1.  The host file is empty so we need to add our target nodes
2.  ```cd /etc/ansible``` 
3.  ``` ls``` you can see 3 files 
4.  we need permissions to write in the hosts file ``` sudo nano hosts``` 
5.  we need to add a group of device name it ``` [web]```
    1. to ping a group specifically replace "all" with "web"
6.  add the public ip address (we're already in the same vnet/vpc as the node so we don't need to use public ip but we need practice for the future).
    1.  to get ansible to configure itself ```localhost ansible_connection=local```
7.  add a label to the ip address
8.  add ```ansible_host=*node public ip address*```
9.  add ```ansible_user=ubuntu```
10. add ```private_key_key=~/.ssh/tech264-anjy-aws-key.pem```
![alt text](images/hostsimage-4.png)
1.  save and exit
2.  run the ping again - say yes to connect

![alt text](images/pingimage-5.png)

1. to create sub groups within our group
   1. nano back into the hosts file and create a parent group ``[test]``
   2. place ``[web]`` and ``[db]`` as subgroups - ```[test:children] web db```
   ![alt text](images/subgroupsimage-1.png)
   3. ```ansible-inventory --graph``` to see your grouping and the layout
   ![alt text](images/groupingimage-2.png)

## Running ADHOC
4. to run ADHOC - to run a command on a machine that is hosted
5. ```ansible web -a "date"``` to run the date command on the vm under the [web] group
6. It'll return with the output from your target node vm

![alt text](images/adhoc.png)

## Playbook - install nginx + config
1. in the controller vm
2. cd into the ansible folder ```/etc/ansible```
3. sudo nano and make a file ```sudo nano install_nginx.yaml```
4. a yaml file begins with 3 dashes and ends with 3 dots(you can do multiple yaml files within on if you use the "---" and "...")
![alt text](images/yamlimage.png)
1. make it run using ```ansible-playbook install_nginx.yaml```
2. check on your target node that nginx is running 
![alt text](images/targetrunningimage-1.png)

# Use ADHOC to copy to target node
```
ansible web -m ansible.builtin.copy -a "src=~/.ssh/tech264-anjy-aws-key.pem dest=~/.ssh/tech264-anjy-aws-key.pem mode=0400"
```
- the ``web`` to specify your group (or the specific host)
- use the ansible copy modules ```ansible.builtin.copy```
- specify what you want to copy and its path ```src=~/.ssh/tech264-anjy-aws-key.pem```
- specify path you want it to go and the name ```dest=~/.ssh/tech264-anjy-aws-key.pem```
- choose the permissions the file will have ```mode=0400```

# Use a copy a module
1. create a new yaml file in your ansible folder (sudo nano)
2. name it "copy_test_file.yaml"

![alt text](images/copymoduleimage.png)

1. run the playbook ```ansible-playbook copy_test_file.yaml```
2. check your target node home direc


# Playbook - provision the APP VM

1. name the playbook "prov_app_with_npm_start.yaml"

* so far...

![alt text](images/testappvmyamlimage.png)



