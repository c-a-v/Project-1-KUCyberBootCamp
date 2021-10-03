# Project-1-KUCyberBootCamp
## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Diagram/network.topography.SS.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above.
Alternatively, select portions of the playbook files may be used to install only certain pieces of it, such as Filebeat.

  elkplaybook.yaml
  filebeatplaybook.yml
  metricbeat-playbook.yml
  config.web.vm.docker.playbook.yml

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The primary purpose of this network is to expose a load-balanced and monitored instance of DVWA (Damn Vulnerable Web Application).

Load balancing ensures that the application will be highly effecient, in addition to restricting traffic to the network. Load balancers protect the system
from DDoS attacks by rerouting live traffic from one server to another. They help to eliminate single points of failure and make it more difficult to
exhaust resources.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.
- Filebeat monitors the log files or locations you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.
- Metricbeat takes metrics and statistics that it collects and sends them to the output you specify, such as Elasticsearch or Logstash.

The configuration details of each machine may be found below.

| Name                 	| Function   	| IP Address 	| Operating System 	|
|----------------------	|------------	|------------	|------------------	|
| Jump-Box             	| Gateway    	| 10.0.0.1   	| Linux            	|
| Web-1                	| Web Server 	| 10.0.0.5   	| Linux            	|
| Web-2                	| Web Server 	| 10.0.0.6   	| Linux            	|
| red-team-projectVM-1 	| ELK Server 	| 10.1.0.4   	| Linux            	|

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Elk Server machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
70.178.162.229 (my workstation)
5061 Kibana Port

Only the jump box virtual machine can accept connections from the internet. The only IP allowed to acces this machine is the 5061 Kibana Port. Access to
machines within the network can only be gained via the jump box.

A summary of the access policies in place can be found in the table below.

###### NOTE FOR TEACHER GRADING ###### *DELETE LATER*
The table came with the first answer by default (jump box). It says yes/no. Was it asking us to put the correct answer or was yes/no the answer itself?
Because while this isn't publicly accessible, in a way it is because it can be accessed with the proper RSA key, whereas the other VM's can only be accessed
via the jump box. I would greatly appreciate a response in the comments, if possible, or I can get an answer during office hours :). Thanks!

| Name                 	| Publicly Accessible 	| Allowed IP Addresses              	|
|----------------------	|---------------------	|-----------------------------------	|
| Jump Box             	| Yes/No              	| 10.0.0.1  10.0.0.2                	|
| Web-1                	| No                  	| 10.0.0.4                          	|
| Web-2                	| No                  	| 10.0.0.4                          	|
| red-team-projectVM-1 	| Yes                 	| 70.178.162.229 , 5061 Kibana Port 	|

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because of ansible's
simplicity. It is easy to set up and use without prior coding knowledge. Along with being a free, open source tool, it allows for the creation of complex
IT workflows, arrangement of the entire application environment, regardless of where you want it deployed; it is highly customizable. Ansible does not
require any other extra software or firewall ports on the systems you wish to automate. Without the need of extra software, your server is left with more
room for application resource.

The playbook implements the following tasks:

- Install docker.io
-- Install pip3
--- Install Docker python module
---- Increase virtual memory
----- Download and launch a docker

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/docker-success.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
Web-1 | 10.0.0.5
Web-2 | 10.0.0.6

We have installed the following Beats on these machines:
-Microbeats

These Beats allow us to collect the following information from each machine:
Metricbeat - collects our virtual machine's metrics e.g. 'uptime'
Filebeat - collects data about the file system

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:

- Copy the playbook file to Ansible Control Node.

- Update the hosts file to include webserver and elk

- Run the playbook and navigate to Kibana (http://[Host-IP]/app/kibana#/home) to ensure the installation worked as expected.

- The Filebeat-configuration file is the playbook

- Copy [/etc/ansible/files/filebeat-config.yml] to [/etc/filebeat/filebeat.yml]

- Update filebeat-playbook.yml, specify which machine you want to install by updating the host files with the IP addresses of the ELK & Web servers. Then
  select which group to run it on in ansible.

- Navigate to http://[your.ELK-VM.External.IP]:5601/app/kibana in order to check that the ELK server is running.
