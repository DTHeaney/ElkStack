## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![Screenshot (8)](https://user-images.githubusercontent.com/84424172/120985613-c7967b00-c749-11eb-9c1e-eaeb3a8c16a5.png)



These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the yaml file may be used to install only certain pieces of it, such as Filebeat.

  - file

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly efficient, in addition to restricting access to the network
- Load balancers can be set up in a sandbox situation for security purposes, as well JumpBox acts as the first door since it is our gateway into ansible and are other VMS. SSH login required for JumpBox is a good security practice.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log events and system efficiency.
- Filebeat monitors log files, or where it is specified to watch. It colects the log events and forwards them to Elk stack server.
- Metricbeats watchs both the metrics and statistics of the services running on our server.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| ElkStack | SIEM     | 10.1.0.4   | Linux            |
| Wed 1    | VM       | 10.0.0.5   | Linux            |
| web 2    | VM       | 10.0.0.6   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox/Redteamvm machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 66.225.166.27

Machines within the network can only be accessed by SSH connection from JumpBox.
- IP Address: 10.1.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 |  Any                 |
| Web-1    | No                  |  66.225.166.27 10.0.0.4 60.118.185.150 |
| ElkStack | No                  |  66.225.166.27 10.0.0.4/14 10.0.0.0/32 |
| Web-2    | No                  |  66.225.166.27 10.0.0.4 60.118.185.150 |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- The Main advantage automating the confiuration using ansible is that we can use our playbooks to make easy changes to our docker containers, we are also able to easily specify in the hosts file webservers, elk servers, etc..

The playbook implements the following tasks:
- Install filebeat
- path directory
- enable filebeat
- restart filebeat on boot

The following screenshot displays the result of running `docker_ps` after successfully configuring the ELK instance.

![docker_ps_output](https://user-images.githubusercontent.com/84424172/120985486-a9307f80-c749-11eb-9e23-78348761773b.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- web1: 10.0.0.5
- web2: 10.0.0.6

We have installed the following Beats on these machines:
- filebeats
- metric beats

These Beats allow us to collect the following information from each machine:
- filebeats: collects log even data which is sent to our elk stack
- metricbeat: collects metrics and statistics on the services running.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the yaml file to /etc/ansible/roles.
- Update the yaml file to include, install, directory path, enable, restart on boot
- Run the playbook, and navigate to Public Elk Stack Server/Kibana to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook? Where do you copy it?
- filebeat-playbook.yml is the actual playbook file using the command: ansible-playbook filebeat-playbook.yml which is copied to the path /etc/ansible/roles
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?
- The 'hosts' file is where we makes chnages to ansible on which servers to run, and even specify elkstack
- _Which URL do you navigate to in order to check that the ELK server is running?
- http://40.118.185.150:5601/app/kibana#/home

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
