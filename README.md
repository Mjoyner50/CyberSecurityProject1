# CyberSecurityProject1
Setting up a cloud network with Azure

## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

[TODO: Update the path with the name of your diagram](Images/diagram_filename.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the _____ file may be used to install only certain pieces of it, such as Filebeat.

  - filebeat-playbook.yml
  - filebeat-config.yml

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly functional, in addition to restricting high-traffic client requests to the network.

  - What aspect of security do load balancers protect?
    -It helps prevent overloading servers as well as optimizes productivity and maximizes uptime.
    -It also adds resiliency by rerouting live traffic from one server to another causing it to eliminate single points of failure from attacks such as DDoS attack.

  - What is the advantage of a jump box?
    -Jump-box are highly secured computers that are never used for non-admin tasks. -Throughout the years, jump-box has improved into an even more comprehensive/lock-down secure admin workstation to decrease the chances of hackers/malware infection.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the network and system logs_.

  - What does Filebeat watch for?
    -It monitors the log files/locations that you specify and forwards them to Elasticsearch/Logstash for indexing.

  - What does Metricbeat record?
    -It records metrics/statistics data and transports them to the output that you specifics thru Elasticsearch/Logstash.

The configuration details of each machine may be found below.

| Name     | Function | IP Address                                | Operating System |
|----------|----------|-------------------------------------------|------------------|
| Jump Box | Gateway  | 10.0.0.8(Private)/52.170.129.21(Public)   | Linux            |
| Web-1    | Server   | 10.0.0.9                                  | Linux            |
| Web-2    | Server   | 10.0.0.10                                 | Linux            |
| Web-3    | Server   | 10.0.0.11                                 | Linux            |
| Web-4    | ELK Stack| 10.1.0.6(Private)/137.135.25.75(Public)   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jumpbox machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
   - (LocalHostIP)

Machines within the network can only be accessed by the Jumpbox machine.
   - Which machine did you allow to access your ELK VM? 
    -The Jumpbox machine

   - What was its IP address?_
    -10.0.0.8(Private)

Summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses |
|----------|---------------------|----------------------|
| Jump Box | Yes                 | LocalHost Public IP  |
| Elk      |                     | 10.1.0.6             |
| Web-1    | No                  | 10.0.0.9             |
  Web-2    | No                  | 10.0.0.10            |
  Web-3    | No                  | 10.0.0.11            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
   - What is the main advantage of automating configuration with Ansible?_
     -One main advantage would be YAML Playbooks. It is the best alternative for configuration management/automation.
     -It is also able to automate complex multi-tier IT application environemtns.

The playbook implements the following tasks:
   - In 3-5 bullets, explain the steps of the ELK installation play. E.g., install Docker; download image; etc._
    -First, SSH into the Jump-Box-Provisioner (ssh azadim@52.170.129.21)
    -Switch to root (sudo su)
    -View/Start/Attached to the ansible docker (docker container ls -a)/(docker start 'container_name')/(docker attach 'container_name')
    -Go to /etc/ansible directory and create the ELK playbook (install-elk.yml)
    -Ran the "install-elk.yml" in that same directory (ansible-playbook install-elk.yml)
    -Lastly, SSH into the ELK-VM to verify the server is up and running. 
 

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.
#TODO: Add screenshots

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
  - Web-1
  - Web-2
  - Web-3

This network has installed the following Beats on these machines:
  - Filebeat
  - Metricbeat

These Beats allow us to collect the following information from each machine:

  - Filebeat is used to collect log files from specific files on remote machines.

  - Examples of Filebeats can be files that are generated by Apache, Microsoft Azure tools, the Nginx web server, and MySQl databases.

  - Metricbeat collects machine metrics.

  - It is simply a measurement to tell analysts how healthy it is.

  - Examples of Metricbeat can be CPU usage/Uptime


### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
    --Filebeat--
- Copy the filebeat-config.yml file to /etc/ansible.
- Update the filebeat-config.yml file to include the ELK private IP on lines 1105 and 1805.
- Run the playbook, and navigate to http://(elk public IP):5601/app/kibana to check that the installation worked as expected.
    --Metricbeat--
- Copy the metricbeat-config.yml file to /etc/ansible.
- Update the metricbeat-config.yml file to include the ELK private IP in lines 62 and 96.
- Run the playbook, and navigate to http://(elk public IP):5601/app/kibana to check that the installation worked as expected.

 Answer the following questions to fill in the blanks:
  - Which file is the playbook? Where do you copy it?_
    -filebeat-playbook.yml
  - Where does it get copied?
    -/etc/ansible
  - Which file do you update to make Ansible run the playbook on a specific machine? 
    -/etc/ansible/hosts
  - How do I specify which machine to install the ELK server on versus which to install Filebeat on?
    -By updating the hosts file to have a "webserver" group with the private IPs of Web1-3 that will be monitored with filebeat. A second group, "elk" will list the private IP of Web-4 where the ELK stack is installed on.
  - Which URL do you navigate to in order to check that the ELK server is running?
    -http://"(elk public IP):5601/app/kibana 

Setting up Filebeat and Metricbeat. A step by step guide.

1. Create filebeat-config.yml: nano filebeat-config.yml, paste text from provided file and update with correct ip addresses.
2. Create filebeat-playbook.yml: nano filebeat-playbook, paste text from provided file. Verify correct "src" for absoulte path to filebeat-config.yml.
3. Run playbook: "ansible-playbook filebeat-playbook.yml"
4. Create metricbeat-config.yml: nano metricbeat-config.yml, paste text from provided file and update with correct ip addresses.
5. Create metricbeat-playbook.yml: nano metricbeat-playbook, paste text from provided file. Verify correct "src" for absolute path to metricbeat-config.yml.
6. Run playbook: "ansible-playbook metricbeat-playbook.yml"
