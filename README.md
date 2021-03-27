## **Automated ELK Stack Deployment**

The files in this repository were used to configure the network depicted below.

![image](Images/Project_1_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the .yml file may be used to install only certain pieces of it, such as Filebeat.

  - **[.yml_Playbooks](/Ansible)**

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible build


### **Description of the Topology**

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting incoming traffic to the network. 
- Load Balancers can prevent DDoS attacks by managing the flow of traffic ensuring that servers don’t get overwhelmed. 

- A Jump-box is used to create a controlled access point that is only available to system administrators which allows them to access the network while keeping it hidden from the public.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to systems logs and metrics.
- Filebeat is utilized to monitor log files and log events. 
- Metricbeat collects metrics from the OS and active services running on the server.  

The configuration details of each machine may be found below:

|   Name   |     Function     | IP Address |   Operating System   |
|:--------:|:----------------:|:----------:|:--------------------:|
| Jump-Box |      Gateway     |  10.0.0.4  | Linux - Ubuntu 18.04 |
|   Web-1  |    Web Server    |  10.0.0.5  | Linux - Ubuntu 18.04 |
|   Web-2  |    Web Server    |  10.0.0.6  | Linux - Ubuntu 18.04 |
|   Web-3  |    Web Server    |  10.0.0.7  | Linux - Ubuntu 18.04 |
|    Jyn   | Monitoring (ELK) |  10.1.0.4  | Linux - Ubuntu 18.04 |

### **Access Policies**

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP address:
- Administrator’s IP address

The only way machines on the network can be accessed is through the Jump-Box which connects to the servers, including the ELK server, via its internal IP address of 10.0.0.4. 

A summary of the access policies in place can be found in the table below:

|   Name   | Publicly Accessible |  Allowed IP Addresses |
|:--------:|:-------------------:|:---------------------:|
| Jump-Box |          Yes        |       Admin's IP      |
|   Web-1  |          No         |        10.0.0.4       |
|   Web-2  |          No         |        10.0.0.4       |
|   Web-3  |          No         |        10.0.0.4       |
|    Jyn   |          Yes         | 10.0.0.4 & Admin's IP |

### **Elk Configuration**

Ansible was used to automate the configuration of the ELK machine. No configuration was performed manually, which is advantageous because automation not only reduces the chance of errors but also allows multiple machines to be configured at once which is vastly more efficient than manually configuring each machine individually. In addition, the existing files are easy to edit should changes or updates need to be made in the future. 

The playbook implements the following tasks:  **[.yml_Playbook](/Ansible)**

- Install docker.io
- Install python-3-pip
- Install Docker module
- Increase virtual memory 
- Download and launch a docker ELK container
- Enable service docker on boot so that docker starts every time the system is started

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker ps](Images/docker_ps_ss.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1 10.0.0.5
- Web-2 10.0.0.6
- Web-3 10.0.0.7

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat is a log shipper used to tail log files such as audit logs, server logs, slow logs, and deprecation logs. The log data can then either be forwarded to Logstash for more advanced processing or sent directly to Elasticsearch for indexing.
- Metricbeat functions much like Filebeat but instead of log files, Metricbeat ships host metrics such as CPU usage and memory statistics. In environments using containers, Metricbeat can also be used to measure container performance metrics. 

### **Using the Playbook**
To use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

**To install ELK:**

Copy the **[install-elk.yml](/Ansible)** file to /etc/ansible/roles

Add your VM’s IP address to the /etc/ansible/hosts file. This allows Ansible to run the playbook on a specific machine. 

Use the following command to edit the file:

   `nano /etc/ansible/hosts`

Update the file so that your VM’s IP address is listed in the [elk] group. If the [elk] group doesn’t exist yet, add it under the [webservers] group.

The IP address should be followed by: 

ansible_python_interpreter=/usr/bin/python3   (be sure there is a space between this and the IP)

Example:  
/etc/ansible/hosts

```[webservers]

10.0.0.4 ansible_python_interpreter=/usr/bin/python3

10.0.0.5 ansible_python_interpreter=/usr/bin/python3

10.0.0.6 ansible_python_interpreter=/usr/bin/python3

 [elk]
 
 10.1.0.4 ansible_python_interpreter=/usr/bin/python3
```
Now that the /etc/ansible/hosts file has been updated you can run the playbook. 

Use the command:

   `ansible-playbook install-elk.yml`
 
After running the playbook, SSH from your Ansible container to the ELK machine.

From there run the following command to check that seb/elk:761 is running.

   `docker ps` 

The result should be similar to the image below:

 ![image](Images/docker_ps_ss.PNG)
- Navigate to http://<ELK.VM.External.IP>:5601/app/kibana to check that the installation worked as expected. 

***To run the Filebeat Playbook:***

Copy the **[filebeat-playbook.yml](/Ansible)** to /etc/ansible/roles

Copy the **[filebeat-config.yml](/Ansible)** to /etc/ansible/

To edit the filebeat-config.yml file run:

   `nano /etc/ansible filebeat-config.yml`
- Use Ctrl + w to move to line #1106 then replace the IP address with your ELK machines IP
- Move to line #1806 and insert your ELK IP address there as well

To run the playbook use: 

   `ansible-playbook filebeat-playbook.yml`

- Navigate to http://<ELK.VM.External.IP>:5601/app/kibana and check that the playbook ran successfully. You can search for filebeat-* in the Dashboard

If it was successful you should see similar results to those shown below:
![image](/Images/Filebeat_kb_SS.png)

To run the Metricbeat Playbook:

Copy the **[metricbeat-playbook.yml](/Ansible)** to /etc/ansible/roles

Copy the **[metricbeat-config.yml](/Ansible)** to /etc/ansible

To edit the metricbeat-config.yml file run:

   `nano /etc/ansible metricbeat-config.yml`
- Use Ctrl + w to move to line #62 then replace the IP address with your ELK machines IP
- Move to line #94 and insert your ELK IP address there as well

To run the playbook use: 

   `ansible-playbook metricbeat-playbook.yml`

- Navigate to http://<ELK.VM.External.IP>:5601/app/kibana and check that the playbook ran successfully. You can search for metricbeat-* in the Dashboard

If it was successful you should see similar results to those shown below:
![image](/Images/Metricbeat_kb_SS.png)


