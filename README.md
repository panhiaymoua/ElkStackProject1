## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![ElkStack Diagram](Diagrams/ElkStack Diagram.png}

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.
  _[Elk Install] (https://github.com/panhiaymoua/ElkStackProject1/blob/main/Ansible/ELK/elk.yml)
  _[DVWA] (https://github.com/panhiaymoua/ElkStackProject1/blob/main/Ansible/DVWA/DVWA-playbook.yml)
  _[FileBeat] (https://github.com/panhiaymoua/ElkStackProject1/blob/main/Ansible/Filebeat/Filebeat-playbook.yml)
  _[MetricBeat] (https://github.com/panhiaymoua/ElkStackProject1/blob/main/Ansible/Metricbeat/Metricbeat-playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly realiable, in addition to restricting traffic to the network.
- _A jumpbox or bastion server serves as a gatway to gain entry into a remote network. Many times the primary mode of access is ssh and without the key access is forbidden
- _A loadbalancer is meant to serve as a specific point of access for a service that is served by multiple machines. This allows high availability models to function properly
- _A load balancers can defend an organization against denial-of-service (DDos) attacks. The advantage of having a jumpbox is being able to use a virtual machine that has hardended security and can manage other systems within your security sone or overal network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the log files and system resources.
- _Filebeat monitors the log files or locations that you specify. Filebeat is meant primarily to watch for systemlogs and forward any changes to the Host.
- _Metricbeat records the metrics and statistics from the operation system and from services running on the server. Metricbeat is used only for gathering metrics adn system resources uage for display.

The configuration details of each machine may be found below.
_Note: Use the [Markdown Table Generator](http://www.tablesgenerator.com/markdown_tables) to add/remove values from the table_.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.1   | Linux            |
| DVWA-WEB1| server   | 10.0.0.7   | Linux            |
| DVWA-WEB2| server   | 10.0.0.8   | Linux            |
| ELKserver| server   | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- _73.242.125.11

Machines within the network can only be accessed by the Jumpbox.
- _The Jump Box VM has access to the ELK VM. 
    - _The Private IP address of the Jump Box VM is 10.0.0.4 and 
    - _The Public IP is 52.149.182.120.

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | SSH-22 Yes          | 73.242.125.11        |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| ELK      | No                  | 10.0.0.4

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
- _Ansible allows IT administrators to automate their daily tasks and save a lot of time. That frees them to focus on efforts that help deliver more value to the business by spending time on more important tasks.

The playbook implements the following tasks:
- _Install Docker
- _Install python3-pip
- _Install Docker python module
- _Set the vm.max_map_count to 262144
- _Download and launch a docker Elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![docker-ps](Images/docker-ps.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
-10.1.0.4
-10.0.0.7
-10.0.0.8

We have installed the following Beats on these machines:
-_We have installed Filebeat and Metricbeat on the following Systems: Web1, Web2, ELK
  

These Beats allow us to collect the following information from each machine:
- _Filebeat monitors the log files or locations. Metricbeat records the metrics and statistics from the operation system and from services running on the server, which we could use to look at how much RAM or CPU usage was being used on the webservers at certain time.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- _Copy the elk_install.yml file to /etc/ansible/roles/elk_install.yml.
- _Update the hosts file  file to include the attribute, such as [elk], then include your destination ip of the ELK server directly
- _Run the playbook, and navigate to ttp://[your_elk_server_ip]:5601/app/kibana to check that the installation worked as expected.

_As a **Bonus**, provide the specific commands the user will need to run to download the playbook, update the files, etc._
- _On the Jump box run the following command to get the playbook: curl https://github.com/panhiaymoua/ElkStackProject1/blob/main/Ansible/ELK/elk.yml
- _Edit the hosts file in /etc/ansible and add the details and update your IP addresses
- _Run the playbook: ansible-playbook /etc/ansible/elk.yml
- _Check your installation is working by visiting http://[your_elk_server_ip]:5601/app/kibana

- Installing Filebeats:
  - _Download the playbook with the following command: curl https://github.com/panhiaymoua/ElkStackProject1/blob/main/Ansible/Filebeat/Filebeat-playbook.yml
  - _Run the playbook: ansible-playbook /etc/ansible/filebeat-playbook.yml
  
