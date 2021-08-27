## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![alt text](https://github.com/JoshVangor/CyberSecurityProject/blob/main/Diagrams/JoshVangorElkProject.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

[Elk Installation Playbook](https://github.com/JoshVangor/CyberSecurityProject/blob/main/Ansible/install-elk.yml)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application.
Load balancing ensures that the application will be highly accessible, in addition to restricting traffic to the network.
Load Balancers protect against DDOS attacks, if one of the web servers fails from overload, the other server receives all remaining traffic. Using a jump box adds increased security because it receives no outside internet traffic which makes the jump box significantly more difficult to attack. A jump box is also designed to only allow administrative access.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system files.
Filebeat watches for any changes in log files for the entire system or specified locations.
Metricbeat monitors the servers to collect statistics from the OS and the services running on the systems.

###The configuration details of each machine may be found below.

| Name     | Function  | IP       | OS    |
|----------|-----------|----------|-------|
| Jump Box | Gateway   | 10.0.0.4 | Linux |
| Web 1    | DvWA | 10.0.0.5 | Linux |
| Web 2    | DvWA | 10.0.0.6 | Linux |
| ElkVM    | Elk    | 10.1.0.4 | Linux |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the jump-box-provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
IP: 146.168.209.206

Machines within the network can only be accessed by ssh.
Only Webserver machines are allowed to access the ElkVM. The IPs of these machines are 10.0.0.5 (Web-1) and 10.0.0.6. (Web-2).

A summary of the access policies in place can be found in the table below.
| Name       | Publicly Accessible | Allowed IPs         |
|------------|---------------------|---------------------|
| Jump Box   | Yes                 | Personal IP    |
| WebServers | No                  | 10.0.0.4            |
| ElkVM      | Yes                  | 10.0.0.5 , 10.0.0.6 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
This leaves no room for user errors such as typos or syntax mistakes.
The playbook implements the following tasks:
- Install Docker
- Install Python3-pip
- Install Docker Module
- Increase Virtual Memory
- Download and Launch Elk Container
The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![alt text](https://github.com/JoshVangor/CyberSecurityProject/blob/main/Ansible/elkcontainerscreenshot.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1: 10.0.0.5
Web-2: 10.0.0.6

We have installed the following Beats on these machines:
Both Filebeat and Metricbeat were both installed onto the ElkVM.

These Beats allow us to collect the following information from each machine:
Filebeat monitors log files and collects these events for indexing. This will allow us to see logon events and log changes. While Metricbeat will collect metrics from the OS and system services that are running. This will allow us to monitor what services are actively running (e.g., Apache).

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible.
- Update the hosts.yml file to include the ips of the machines you want to install the services on.
- Run the playbook, and navigate to [http://[your.ELK-VM.External.IP]:5601/app/kibana] to check that the installation worked as expected.

### Commands to run
Downloading and running the playbook:
- ansible-playbook /etc/ansible/install-elk.yml

Updating the file:
- sudo nano install-elk.yml
- sudo nano hosts.yml
