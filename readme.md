# ELK-Stack-Project
Project 1 - ELK Stack Project

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](/Diagrams/ELK_diagram.pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml

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
- The load balancer get's the public I.P. address 20.25.1.97 and distributes traffic to the webservers. Load Balancers protect against
denial of service attacks (DDoS) because the load balancer analyzes the traffic coming in and determines 
what server to send the traffic to. This prevents one server from getting overloaded with traffic because the load balancer allows traffic 
to be distributed evenly among the servers that are connected to it. It is also common for load balancers to have a health probe that 
periodically checks that a machine is working properly before sending traffic. If it isn't, the load balancer will divert traffic from the 
malfunctioning server until the issue is resolved. A jump box limits the access that the public has to your virtual network because in order 
to access the other virtual machines, an individual needs the private IPs of the machines. A jumpbox allows greater control over access to 
a virtual network and its contents.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.
- Filebeat looks for changes in files and when they occurred by looking at log files because Filebeat generates and organizes log files.
- Metricbeat records metrics from the Operating system and services running on the server. By using Kibana, you can 
visualize the metrics and statistics that Metricbeat generates from the OS and running services.
The configuration details of each machine may be found below.

| Name         | Function       | IP address | Operating System            |
|--------------|----------------|------------|-----------------------------|
| Jumpbox      | Gateway        | 10.0.0.4   | Linux Ubuntu 18_04-lts-gen2 |
| Load Balancer| Balance W1,2,3 | 20.25.1.97 | Azure Virtual Load Balancer | 
| Web 1        | Webserver      | 10.0.0.5   | Linux Ubuntu 18_04-lts-gen2 |
| Web 2        | Webserver      | 10.0.0.6   | Linux Ubuntu 18_04-lts-gen2 |
| Web 3        | Webserver      | 10.0.0.7   | Linux Ubuntu 18_04-its-gen2 |
| ELK Server   | Running E.L.K. | 10.1.0.5   | Linux Ubuntu 18_04-lts-gen2 |


### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 135.180.116.70 (Administrator's IP)

Machines within the network can only be accessed by the Jumpbox.
- Only the Administrator's computer 135.180.116.70 is able to access the ELK server.

A summary of the access policies in place can be found in the table below.

| Name          | Publicly Accessable | Allowed IP addresses |
|---------------|---------------------|----------------------|
| Jumpbox       | Yes, via port 22    | 135.180.116.70       |
| Web 1         | No                  | 10.0.0.4             |
| Web 2         | No                  | 10.0.0.4             |
| Web 3         | No                  | 10.0.0.4             |
| ELK Server    | Yes, via port 5601  | 135.180.116.70       |
| Load Balancer | Yes, via port 80    | 20.25.1.97      |

### Elk Configuration

Ansible was used to automate configuration of the ELK server. No configuration was performed manually, which is advantageous because...
- It eliminates human error in setting up the web servers and makes deploying more very quick and easy

The playbook implements the following tasks:
- The first step in setting up the ELK server was installing Docker on the ELK server
- Python was installed next
- Configure the ELK server to install and execute 'docker up' on start-up of the ELK server

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](/ELK_screenshot_docker_ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-Web1 10.0.0.5
-Web2 10.0.0.6
-Web3 10.0.0.7

We have installed the following Beats on these machines:
- Filebeats and Metricbeats were installed 

These Beats allow us to collect the following information from each machine:
- Filebeats monitors for changes to files and their locations. Changes are logged and sent to Elasticsearch and Logstash or review and indexing.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml file to /etc/ansible/files.
- Update the configuration file to include the private IP of the ELK server in Elasticsearch and Kibana
- Run the playbook, and navigate to http://104.42.158.168:5601/app/kibana to check that the installation worked as expected.


- elk-install.yml installs the ELK server
- /etc/ansible/hosts is the file updated to make Ansible fun the playbook on a specific machine
- Navigate to http://104.42.158.168:5601/app/kibana to verify that the ELK server is running.

