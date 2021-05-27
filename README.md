## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://github.com/LukeGonzaga39/CybersecurityProjects/blob/main/Diagrams/ElkStackDiagram.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.
  
  https://github.com/LukeGonzaga39/CybersecurityProjects/blob/main/Ansible/ConfigureWebServersWithDVWA.yml
  https://github.com/LukeGonzaga39/CybersecurityProjects/blob/main/Ansible/elk-playbook.yml
  https://github.com/LukeGonzaga39/CybersecurityProjects/blob/main/Ansible/filebeat-playbook.txt
  https://github.com/LukeGonzaga39/CybersecurityProjects/blob/main/Ansible/metricbeat-playbook.yml
  

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly secure, in addition to restricting traffic to the network.
What aspect of security do load balancers protect? What is the advantage of a jump box? Load balancers protect the systems in the network from distributed denial of service attacks by moving the attack traffic. 
A Jump box is advantageous as it serves as an extra layer of security seperate to the firewall, essentially it is the first computer you connect to to gain access to all the other computers in the network. 

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the configuration and system files.
What does Filebeat watch for? Logfiles
What does Metricbeat record? Metric Logs

The configuration details of each machine may be found below.

| Name     | Function | IP Address | Operating System |
|----------|----------|------------|------------------|
| Jump Box | Gateway  | 10.0.0.4   | Linux            |
| Web-1    | Server   | 10.0.0.5   | Linux            |
| Web-2    | Server   | 10.0.0.6   | Linux            |
| Web-3    | Server   | 10.0.0.7   | Linux            |
| Elk      | Monitoring | 10.1.0.4 | Linux            |
### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump-Box-Provisioner machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
5601 Kibana port

Machines within the network can only be accessed by Jump-Box-Provisioner via Ansible container.
Which machine did you allow to access your ELK VM? What was its IP address? Jump-Box-Provisioner Private IP: 10.0.0.4

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | 40.127.81.167        |
| Web-1    | No                  | 10.0.0.4             |
| Web-2    | No                  | 10.0.0.4             |
| Web-3    | No                  | 10.0.0.4             |
| Elk      | No                  | 10.0.0.4             |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
What is the main advantage of automating configuration with Ansible?_

The playbook implements the following tasks:
- Install docker.io
- Install python3-pip
- Install docker module
- Increase virtual memory
- Use more memory
- download and launch a docker elk container
- Enable docker service

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![](https://github.com/LukeGonzaga39/CybersecurityProjects/blob/main/Images/SuccessfulElkDeployment.PNG)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
       | Name  	    |   	| IP Address 	|
       |------------|	    |-------------|
       | Web-1 	    |   	| 10.0.0.5   	|
       | Web-2 	    |   	| 10.0.0.6   	|
       | Web-3 	    |   	| 10.0.0.7   	|

We have installed the following Beats on these machines:
- Filebeat
- Metricbeat

These Beats allow us to collect the following information from each machine:
Firstly filbeat collects the data from the system such as log events and provide a visual representation of the data through elks gui in the kibana application. Metricbeat collects metrics and statistics which is then outputted through Elastisearch and Logstash.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the playbook or yaml file to the Ansible container.
- Update the host file to include all Webservers including Elk.
- Run the playbook, and navigate to the kibana web page to check that the installation worked as expected.

Specific commands the user will need to successfully the playbook and have it configured for the specified VM's

- nano -l ansible.cfg (-l to see line numbers)
- add the machine, its IP, and ansible_python_interpreter=/usr/bin/python3 to the hosts
- Ctrl + x then y to save and exit the file
- nano -l elk-playbook.yml /home (or whatever directory you have made this file in the ansible container)
- name: installing elk hosts: [your_machine]
- Ctrl + x then y to save and exit the file
- ansible-playbook elk-playbook.yml
