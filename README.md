## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ELK Stack Diagram](https://github.com/Calvin-R/Cyber-Security-Repository/blob/main/Diagrams/ELK%20Project%20Network%20Diagram(1).pdf)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to recreate the entire deployment pictured above. Each playbook has its own file so that, if you wish, you can install only certain pieces of it, such as Filebeat.

 ![Playbook Files](https://github.com/Calvin-R/Cyber-Security-Repository/tree/main/Ansible)

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be more secure, in addition to restricting unauthorized access to the network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system traffic.

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump-Box-Provisioner | Gateway  | 10.0.0.4   | Linux            |
| Web-1    |Web Server|10.0.0.6    |Linux             |
| Web-2    |Web Server|10.0.0.5    |Linux             |
| ELK-Server|Database  |10.1.0.4   |Linux             |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from my personal IP address because I configured the network security group to only allow SSH access from my IP.

Machines within the network can only be accessed by the Jump-Box-Provisioner.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump-Box-Provisioner | No                  | My personal IP address    |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because the use of playbooks written in YAML they are easy to read, update, and delpoy. This makes the configuration easier to implement at large or small scales.

The playbook implements the following tasks:
- Install docker.io
- Install pip3
- Install docker python module
- Use more memory
- Download and launch a docker container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- Web-1
- Web-2

We have installed the following Beats on these machines:
- Filebeats
- Metricbeats

These Beats allow us to collect the following information from each machine:
- Per Elastic, "Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing." It will also configure the Elastic search in Kibana so that you have all the correct ingest node pipelines, dashboards, and patterns needed to get started.
- Elastic's description of their Metricbeat tool states, "Metricbeat helps you monitor your servers by collecting metrics from the system and services running on the server." It is a more generalized tool and allows you to select which metrics you want to collect.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the .yml playbook files linked above to the /etc/ansible folder in your ansible container.
- Edit the webservers portion of ansible host file to include the IP addresses of you web servers, and create a separate [elkserver(s)] section to do the same for the ELK server. The entry should appear as follows: [your.VM.IP] ansible_python_interpreter=/usr/bin/python3
- Run the playbooks, and then navigate to http:[load-balancer-ip]/setup.php to check that the installation worked as expected for the web servers. To verify that you can load the ELK stack server, navigate to http://[your.VM.IP]:5601/app/kibana
