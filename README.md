## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![image](Images/Project_1_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - [Playbooks](/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting incoming traffic to the network.

Load balancing ensures that the application will be highly available, in addition to restricting incoming access to the network. They also prevent DDoS attacks by managing the flow of traffic ensuring that servers don’t get overwhelmed. 

Using a Jump-box to create a controlled access point allows administrators access to the network while keeping it hidden from the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems and system metrics.
- Filebeat us utilized to monitor log files. Its creators describe it as being used for "forwarding and centralizing log data." Once that data has been collected it can then be parsed and visualized for easy interpretation.
- Metricbeat is useful in capturing system and service statistics. It periodically collects metrics from the OS and active services on the server to help users keep track of the system’s workings whether it be CPU, memory, or applications.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

|   Name   |     Function     | IP Address |   Operating System   |
|:--------:|:----------------:|:----------:|:--------------------:|
| Jump-box |      Gateway     |  10.0.0.4  | Linux - Ubuntu 18.04 |
|   Web-1  |    Web Server    |  10.0.0.5  | Linux - Ubuntu 18.04 |
|   Web-2  |    Web Server    |  10.0.0.6  | Linux - Ubuntu 18.04 |
|   Web-3  |    Web Server    |  10.0.0.7  | Linux - Ubuntu 18.04 |
|    Jyn   | Monitoring (ELK) |  10.1.0.4  | Linux - Ubuntu 18.04 |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- Administrator’s (Rey) personal IP address


Machines within the network can only be accessed by Jump-Box.
- 

A summary of the access policies in place can be found in the table below.

|   Name   |     Function     | IP Address |   Operating System   |
|:--------:|:----------------:|:----------:|:--------------------:|
| Jump-box |      Gateway     |  10.0.0.4  | Linux - Ubuntu 18.04 |
|   Web-1  |    Web Server    |  10.0.0.5  | Linux - Ubuntu 18.04 |
|   Web-2  |    Web Server    |  10.0.0.6  | Linux - Ubuntu 18.04 |
|   Web-3  |    Web Server    |  10.0.0.7  | Linux - Ubuntu 18.04 |
|    Jyn   | Monitoring (ELK) |  10.1.0.4  | Linux - Ubuntu 18.04 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- Automation not only reduces the chance of errors but also allows multiple machines to be configured at once which is vastly more efficient than manually configuring each machine individually. In addition, automation

The playbook implements the following tasks:
- Install docker.io
- Install python-3-pip
- Install Docker module
- Increase virtual memory 
- Download and launch a docker elk container
- Enable service docker on boot



The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](Images/docker_ps_ss.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the _____ file to _____.
- Update the _____ file to include...
- Run the playbook, and navigate to ____ to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?_
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
- _Which URL do you navigate to in order to check that the ELK server is running?

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
