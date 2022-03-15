# Project-1-ELK-Stack
Week 13 Project 1 ELK Stack

These files have been tested and used to generate a live ELK deployment on Azure.

https://drive.google.com/file/d/1l5C0C4v-OkielLdi5PAGi-1bg0e1WFoX/view?usp=sharing

They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible playbook file may be used to install only certain pieces of it, such as Filebeat.

Enter the playbook file:

- Install ELK:
https://github.com/ev2000/Project-1-ELK-Stack/blob/main/Ansible/elkplaybook.yml

- Hosts: https://github.com/ev2000/Project-1-ELK-Stack/blob/main/Ansible/Hosts

- Ansible:
https://github.com/ev2000/Project-1-ELK-Stack/blob/main/Ansible/ansible.cfg

This document contains the following details:

Description of the Topologu
Access Policies
ELK Configuration
Beats in Use
Machines Being Monitored
How to Use the Ansible Build

Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available , in addition to restricting access to the network.

 - What aspect of security do load balancers protect? - The load balancer protects against DDoS (Denial of service) attacks, SSL offload, authenticate user ID, protects applications from threats, traffic compression, and traffic cashing.

 - What is the advantage of a jump box? - Acts as an audit for traffic and a single point where we can manage user accounts.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the data and system logs.

 - What does Filebeat watch for? - Filebeat monitors for log files, collects log events, and forwards that information to Elasticsearch, or Longstash for indexing.

 - What does Metricbeat record? - Metricbeat records metrics and statistics, and sends the output to programs such as Elasticsearch or Logstash.

The configuration details of each machine may be found below. Note: Use the Markdown Table Generator to add/remove values from the table.

| Name      | Function          | IP Address | Operating System |
|-----------|-------------------|------------|------------------|
| Jump Box  | Gateway           | 10.0.0.7   | Linux            |
| Web-1     | Web Server        | 10.0.0.8   | Linux            |
| Web-2     | Web Server        | 10.0.0.9   | Linux            |
| ELK-Stack | Monitoring Server | 10.1.0.4   | Linux            |

Access Policies

 - The machines on the internal network are not exposed to the public Internet.

 - Only the jump box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

 - Add whitelisted IP addresses - Personal public IP address

 - Machines within the network can only be accessed by - jump box provitioner.

 - Which machine did you allow to access your ELK VM? - jump box provitioner.

 - What was its IP address? - 10.1.0.4

 - The Jump-Box-provitioner is able to connect via SSH to the Elk-Stack machine through port 22. In addition the Personal Host IP address is also able to access the Elk-Stack machine through port 5601

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses |
|-----------|---------------------|----------------------|
| Jump Box  | Yes                 | Public IP, 10.0.0.7  |
| Web-1     | No                  | 10.0.0.8             |
| Web-2     | No                  | 10.0.0.9             |
| ELK-Stack | Yes/No              | Public IP, 10.1.0.4  |
| Load-Bal  | Yes                 | 20.124.231.20        |

Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because - System installation and updates can be done efficiently.

What is the main advantage of automating configuration with Ansible? - Ansible is very easy to set up and use, easy to read, no special coding skills are needed, and is open source (free).
The playbook implements the following tasks:

- Install-ELK

In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc:

- name: set maximum map count in sysctl/systemd

- name: docker.io

- name: instal pip3

- name: Install Docker module

- name: download and launch elk

The following screenshot displays the result of running docker ps after successfully configuring the ELK instance.



Target Machines & Beats

This ELK server is configured to monitor the following machines:

- List the IP addresses of the machines you are monitoring: Web-1 10.0.0.5 , Web-2 10.0.0.6

We have installed the following Beats on these machines: -Specify which Beats you successfully installed: Filebeat , Metricbeat

These Beats allow us to collect the following information from each machine: -In 1-2 sentences, explain what kind of data each beat collects, and provide 1 example of what you expect to see. E.g., Winlogbeat collects Windows logs, which we use to track user logon events, etc.

- Filebeat: Monitors log files and collects log events and then forwards them to Elasticsearch, or Logstash, or any other specified destination. The filebeat would look at the log events and send them to ELK-Stack VM.

- Metricbeat: Takes the metrics and statistics collected and sends them out to programs such as Elasticsearch or Logstash, or any other specified destination. The metricbeat would look at the uptime of the system or the system logs.

Using the Playbook

In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

filebeat-playbook.yml playbook nano file - Once the file created, we need to run the command line (ansible-playbook filebeat-playbook.yml)

- filebeat-playbook.yml: https://github.com/ev2000/Project-1-ELK-Stack/blob/main/Ansible/filebeat-playbook.yml

metricbeat-playbook.yml playbook nano file - Once the file created, we need to run the command line (ansible-playbook metricbeat-playbook.yml)

- filebeat-playbook.yml (i put my metricbeat playbook in the same playbook as my filebeat): https://github.com/ev2000/Project-1-ELK-Stack/blob/main/Ansible/filebeat-playbook.yml

SSH into the control node and follow the steps below:

 - Copy the filebeat-config.yml file to /etc/ansible/files

 - Update the /etc/ansible /hosts file to include the ip address of the webserversand the elk-stack.

 - Run the playbook, and navigate to: http://[personal vm IP]:5601/app/kibana to check installation.

Bonus

 - As a Bonus, provide the specific commands the user will need to run to download the playbook, update the files, etc:

 - Open git bash, then ssh azadmin@jump box ip <----------(My Azure jump-box)

 - sudo docker container list -a <----------(my container name is: quizzical_solomon)

 - sudo docker start quizzical_solomon <----------(start my container)

 - docker attach quizzical_solomon <----------(attach my container)

 - cd /etc/ansible/ <----------(to work under ansible file)

 - ssh-keygen to your web server <----------(get the ssh_rsa.pub key in order to connect)

 - Create a playbook file <----------(use touch to create a nano playbook file)

 - nano hosts <----------(update ip on [webservers][elk][elkservers] Example: 10.1.0.4 ansible_python_interpeter=/usr/bin/python3

 - nano ansible.cfg <----------(add remote_user=azureuser to which server you want to use)

 - run ansible-playbook my-playbook.yml <----------(ansible-playbook is the command to run the file)
