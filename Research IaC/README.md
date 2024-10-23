# Table of Contents
- [Table of Contents](#table-of-contents)
- [What is IaC?](#what-is-iac)
- [Benefits of IaC?](#benefits-of-iac)
- [When/where to use IaC](#whenwhere-to-use-iac)
- [What are the tools available for IaC?](#what-are-the-tools-available-for-iac)
- [What is configuration management (CM)?](#what-is-configuration-management-cm)
- [What is provisioning of infrastructure? Do CM tools do it?](#what-is-provisioning-of-infrastructure-do-cm-tools-do-it)
- [What is Ansible and how does it work?](#what-is-ansible-and-how-does-it-work)
- [Who is using IaC and Ansible in the industry](#who-is-using-iac-and-ansible-in-the-industry)


# What is IaC?
Infrastructure as Code is the practice of managing and setting up computing infrastructure (such as networks, virtual machines, load balancers, and connection topologies) through machine-readable configuration files, rather than physical hardware or interactive configuration tools.

**Key Concepts of IaC:**

1. Declarative vs Imperative:

Declarative: You define the desired state of your infrastructure (e.g., "I want 3 instances running"), and the IaC tool figures out how to achieve that.

Imperative: You provide explicit instructions on how to reach the desired state (e.g., "Create an instance, configure it, etc.").

2. Version Control:

IaC configurations can be version-controlled just like application code, enabling collaboration, auditing, and rollback features.

3. Automation:

IaC automates the provisioning of infrastructure, reducing manual errors and allowing repeatable deployments across environments.

**Types of IaC:**

Mutable Infrastructure: Changes are applied directly to existing resources, updating them in place.

Immutable Infrastructure: When changes are needed, the existing infrastructure is destroyed and recreated from scratch with the new configuration.

# Benefits of IaC?
- Consistency: Ensures identical environments across development, testing, and production, minimizing "it works on my machine" issues.
- Speed: Rapid provisioning of infrastructure, reducing setup times for environments.
- Scalability: Easily scale up or down resources with minimal manual intervention.
- Versioning: Track infrastructure changes over time and roll back to previous states if necessary.
- Cost-Effectiveness: Eliminates the need for manual infrastructure configuration, reducing human errors and associated costs.

# When/where to use IaC

When (how much time is it gonna save me? how often do i need to do this thing? what can turn into commands that i can run to make things? can i make into a script? can i use infrastructure as code to speed it up?):
-  For automating infrastructure
-  Maintaining consistency across environments
-  Scaling infrastructure
-  Disaster recovery
-  CI/CD pipelines
  
Where: 
- In cloud environments (AWS, Azure, Google Cloud)
- Containerized and microservices architectures (Kubernetes, Docker)
- Hybrid and multi-cloud setups
- Serverless infrastructures
- Dynamic test environments

# What are the tools available for IaC?

**Configuration management tool:**
(written in language that the tool understands and then it goes away and configures it how you'd like)
- Ansible – A configuration management tool that can be used for IaC.
- Puppet and Chef – Imperative configuration management tools.

**Orchestration tool:**
(manages the sequences of things that it needs to do, what is dependent of what? what goes first come next?)
- Terraform (HashiCorp) – A declarative tool that supports multiple cloud providers.
- AWS CloudFormation – AWS’s native IaC service for managing AWS resources.
- Azure Resource Manager (ARM) Templates – Azure’s declarative IaC service.

# What is configuration management (CM)?
Configuration Management is the process of systematically handling changes in a system to ensure that it maintains its integrity over time. it manages the configuration of infrastructure, applications, and systems to ensure consistency, reliability, and security.
- installing packages
- configuring software that is already running

**Key Components of Configuration Management:**
- Identification: Define and document the configurations of various components, such as servers, network devices, software, and applications.

- Control: Ensure that only approved changes are made to configurations, often through version control and approval processes.

- Monitoring: Continuously track the state of configurations to ensure they remain as expected.

- Auditing: Verify that the actual state of systems matches the desired configuration.


# What is provisioning of infrastructure? Do CM tools do it?

The process of setting up and configuring the resources and components needed to run applications, services, or systems.

 This includes creating servers, storage, networking components, databases, and other required infrastructure elements. 
 
 Provisioning can occur both on-premise (physical hardware) and in the cloud (virtualized resources like AWS, Azure, or Google Cloud).

Some Configuration Management (CM) tools can handle basic infrastructure provisioning.


# What is Ansible and how does it work?

Ansible is an open-source automation tool used for configuration management, application deployment, orchestration, and task automation. 

It simplifies IT processes by allowing infrastructure and applications to be described as code, making it easier to manage environments consistently and at scale.

Ansible uses a declarative approach, meaning you define the desired state of systems, and Ansible takes care of enforcing that state.

**How Ansible Works:**
Ansible operates by connecting to your nodes (servers, cloud instances, network devices, etc.) via SSH (for Linux/Unix systems) or WinRM (for Windows systems) and executing tasks defined in playbooks. 

It uses an agentless architecture, meaning you don’t need to install any software on the nodes it manages. 

**Key Concepts in Ansible:**

- Playbook: A YAML file where you define automation tasks and configurations. Playbooks describe a series of steps to bring systems to the desired state.

- Tasks: Individual actions within a playbook, such as installing software, configuring services, or modifying files.

- Inventory: A file or dynamic source where you define the hosts or nodes that Ansible will manage. The inventory can be static (a list of servers) or dynamic (generated from a cloud provider).

- Modules: Reusable units of code that perform actions such as installing software, managing files, or interacting with cloud providers. Ansible comes with many built-in modules for various tasks (e.g., managing users, services, and databases).

- Roles: A collection of tasks, files, variables, and handlers organized for reuse across different playbooks or projects.

- Handlers: Tasks that only run when notified by other tasks, usually to restart services after a configuration change.

- Facts: Information gathered about the target system (e.g., IP addresses, OS version) that can be used to make decisions in playbooks.

# Who is using IaC and Ansible in the industry
Ansible and IaC are widely used across industries, especially where scalability, consistency, and automation are essential for operational efficiency.

1. Technology and Cloud Providers:

- Netflix: Uses IaC and Ansible to manage its massive, highly scalable cloud infrastructure in AWS. Automation helps Netflix continuously deliver new features and maintain service reliability.

- Amazon (AWS): AWS provides CloudFormation for IaC, and many of its customers use Ansible to manage and provision AWS infrastructure for scaling applications and cloud services.

2. Finance and Banking:

Goldman Sachs: Uses Ansible and IaC tools to automate infrastructure management, ensuring that cloud and on-premises data centers are secure and compliant with industry regulations.

3. Telecommunications:

AT&T: Implements IaC and Ansible to automate the management and configuration of network infrastructure, ensuring that network devices and services are configured consistently across vast geographic areas.

4. E-commerce:

Etsy: Manages its AWS cloud infrastructure using Ansible and other IaC tools to scale applications, handle deployments, and maintain system configuration.

5. Media and Entertainment:

Sony: Automates its cloud infrastructure using Ansible, ensuring that its services and applications are deployed efficiently across various data centers.

