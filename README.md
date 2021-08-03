## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

!(https://github.com/lizmovius/BootcampProject1/blob/main/Diagrams/Project1_Diagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.

!(https://github.com/lizmovius/BootcampProject1/blob/main/Ansible/Config_WebVM_Docker.txt)
!(https://github.com/lizmovius/BootcampProject1/blob/main/Ansible/Config_ELK.txt)
!(https://github.com/lizmovius/BootcampProject1/blob/main/Ansible/Config_Filebeat.txt)
!(https://github.com/lizmovius/BootcampProject1/blob/main/Ansible/Config_Metricbeat.txt)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the metrics, files, and system logs.

The configuration details of each machine may be found below.

| Name         | Function | IP Address    | Operating System |
|--------------|----------|---------------|------------------|
| Jump Box     | Gateway  | 13.68.158.203 | Linux            |
| Web-1        | DVWA     | 10.0.0.5      | Linux            |
| Web-2        | DVWA     | 10.0.0.6      | Linux            |
| Project-1-VM | ELK      | 10.2.0.4      | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box can accept connections from the Internet. Access to this machine is only allowed from the IP address of the local machine.

Machines within the network can only be accessed by the Jump Box (13.68.158.203).

A summary of the access policies in place can be found in the table below.

| Name         | Publicly Accessible | Allowed IP Addresses                        |
|--------------|---------------------|---------------------------------------------|
| Jump Box     | No                  | Current IP of local machine                 |
| Web-1        | No                  | 13.68.158.203 10.0.0.7                      |
| Web-2        | No                  | 13.68.158.203 10.0.0.7                      |
| Project-1-VM | No                  | 13.68.158.203 10.0.0.7                      |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because automation is more efficient.

The playbook implements the following tasks:
- Install Docker
- Install pip3
- Install Docker Python module
- Increase virtual memory
- Download and launch a Docker ELK container
- Enable Docker on boot

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

!(https://github.com/lizmovius/BootcampProject1/blob/main/Images/Project1ScreenCapture.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines: 
- Web 1 (10.0.0.5)
- Web 2 (10.0.0.6)

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:

Filebeat monitors system logs including sudo commands, SSH sessions, and new users/groups. Metricbeat reports metrics corresponding with the module in use. In this case, it is used with the Docker module, so it pulls metrics from the Docker containers. These include CPU and disk usage, network, memory, etc.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the config file to the etc directory of Web-1 and Web-2.
- Update the hosts file to include the IP addresses of Web-1 and Web-2 under the webservers heading (the IP address of Project-1-VM should go under the ELK heading to allow separate playbooks to be run on it).
- Run the playbook, and navigate to http://[IP]:5601/app/kibana#/home to check that the installation worked as expected.
