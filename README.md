

The files in this repository were used to configure the network depicted below.

![TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - _TODO: Enter the playbook file._

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting inbound access to the network.
- _TODO: What aspect of security do load balancers protect? What is the advantage of a jump box?_ Load Balancing ensures availability to the web-servers which is the availability aspect of security in regards to the CIA Triad.The main advantage of using a JumpBox is having one origination point for administrative tasks. This ultimately sets the JumpBox as a Secure Admin Workstation (SAW). In order to conduct administrative tasks administrators are required to access the JumpBox before accessing the other servers

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the file systems of the VMs on the network and system system metrics.
- _TODO: What does Filebeat watch for?_ Filebeat watches for log files/locations and collect log events. (Filebeat: Lightweight Log Analysis & Elasticsearch)
- _TODO: What does Metricbeat record?_ Metricbeat records metrics and statistical data from the operating system and from services running on the server (Metricbeat: Lightweight Shipper for Metrics)

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
| -------- | -------- | ---------- | ---------------- |
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| DVWA 1   | WServer  | 10.0.0.5   | Linux            |
| DVWA 2   | WServer  | 10.0.0.6   | Linux            |
| Elk      | Monitor  | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet.

Only the jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _TODO: Add whitelisted IP addresses_ 98.116.94.137

Machines within the network can only be accessed by each other.
- _TODO: Which machine did you allow to access your ELK VM? What was its IP address?_ JumpBox was the VM thats accessed my ELK VM. The IP address is 40.121.44.209

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
| -------- | ------------------- | -------------------- |
| Jump Box | Yes/No              | 98.116.94.137        |
| Elk      | No                  | 10.0.0.1-254         |
| DVWA 1   | No                  | 10.0.0.1-254         |
| DVWA 2   | No                  | 10.0.0.1-254         |
### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because... we could deploy multiple servers easily and quickly without having to physically touch each server.
- _TODO: What is the main advantage of automating configuration with Ansible?_ The main advantage of automating the installation process is that we could deploy multiple servers easily and quickly without having to physically touch each server.

The playbook implements the following tasks:
- _TODO: In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
- ...Install Docker.io and pip3
- ...Increases VM memory
- ...Download and Configure elk docker container
- ...Sets Published Ports

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](Images/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- _TODO: List the IP addresses of the machines you are monitoring_
  Redteam-Web1 10.0.0.5
  Redteam-Web2 10.0.0.6

We have installed the following Beats on these machines:
- _TODO: Specify which Beats you successfully installed_
  Filebeat snd Metricbeat

These Beats allow us to collect the following information from each machine:
- _TODO: In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., `Winlogbeat` collects Windows logs, which we use to track user logon events, etc._
  Filebeat watches for log files/locations and collect log events. (Filebeat: Lightweight Log Analysis & Elasticsearch)
  Metricbeat records metrics and statistical data from the operating system and from services running on the server (Metricbeat: Lightweight Shipper for Metrics)

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:
- Copy the filebeat-config.yml and metricbeat-config.yml file to /etc/ansible/files.
- Update the configuration file to include the private IP of the ELK-Server to the ElasticSearch and Kibana Sections of the Configuration File
- Run the playbook, and navigate to Elk Server (Public IP:5601/app/kibana) to check that the installation worked as expected.

_TODO: Answer the following questions to fill in the blanks:_
- _Which file is the playbook?_
  elk-playbook.yml - used to install ELK Server
  filebeat-playbook.yml - used to install and configure Filebeat on Elk Server and DVWA servers
  metricbeat-playbook.yml - used to install and configure Metricbeat on Elk Server and DVWA servers
  -_Where do you copy it?_
  /etc/ansible/
- _Which file do you update to make Ansible run the playbook on a specific machine? How do I specify which machine to install the ELK server on versus which to install Filebeat on?_
  /etc/ansible/hosts.cfg
- _Which URL do you navigate to in order to check that the ELK server is running?_
  http://publicip(elkserver):5601

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
ssh RedAdmin@JumpBox(PrivateIP)
sudo docker container list -a - Locate the ansible container
sudo docker start (Funny_Name)
sudo docker attach (Funny_Name)
cd /etc/ansible
ansible-playbook elk-playbook.yml (Installs and Configures ELK-Server)
cd /etc/ansible/
ansible-playbook beats-playbook.yml (Installs and Configures Beats)
Open a new browser on Personal Workstation, navigate to (ELK-Server-PublicIP:5601/app/kibana) - This will bring up Kibana Web Portal