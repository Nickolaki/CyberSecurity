## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below. 

- [Network Map](https://github.com/Nickolaki/CyberSecurity/blob/main/Files/Map.PNG)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the ansible file may be used to install only certain pieces of it, such as Filebeat.

- [Filebeat Playbook](https://github.com/Nickolaki/CyberSecurity/blob/main/Ansible/Playbooks/filebeats_playbook.yml)

This document contains the following details:
- Description of the Topologu
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly available, in addition to restricting traffic to the network.

- Load balancing is effective at preventing DDoS attacks. The advantage   of the Jump Box is to provide a gateway router to your private network ensuring that all of your other machines in the network do not directly face the internet. This then provides a more secure network.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the Network and system Logs.

- Filebeat monitors the log files or locations that you specify, collects log events, and forwards them either to Elasticsearch or Logstash for indexing.

- metric data from your target servers, this could be operating system metrics such as CPU or memory or data related to services running on the server. It can also be used to monitor other beats and ELK stack itself.

The configuration details of each machine may be found below.


| Name       | Function | Ip Address | Operating System |
|------------|----------|------------|------------------|
| Jump Box   | Ansible  | 10.0.0.4   | Linux            |
| Web_1      | DVWA     | 10.0.0.7   | Linux            |
| Web_2      | DVWA     | 10.0.0.8   | Linux            |
| Elk-Server | Elk      | 10.1.0.4   | Linux            |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:

- 120.17.224.15

Machines within the network can only be accessed by Jump box.
The ELK server can be accessed from the Web DVWA Servers and Jump Box machines.

A summary of the access policies in place can be found in the table below.

| Name       | Publicly Accessible | Allowed IP Addresses     |
|------------|---------------------|--------------------------|
| Jump Box   | Yes                 |      120.17.224.15       |
| Web_1      | No                  |      10.0.0.1-254        |
| Web_2      | No                  |      10.0.0.1-254        |
| Elk-Server | No                  |      10.0.0.1-254        |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because...
The main advantage of automating configuration with Ansible is that it enables IT administrators the ability to automate your daily work tasks and give the administrator more time to focus on the needs of the business.

The playbook implements the following tasks:

- Configure Elk VM with Docker
- Install docker.io
- Install pip3
- Download and launch a docker elk container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

![TODO: Update the path with the name of your screenshot of docker ps output](https://github.com/Nickolaki/CyberSecurity/blob/main/Files/docker_ps_output.png)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:

- Web_1 10.0.0.7
- Web_2 10.0.0.8 

We have installed the following Beats on these machines:

- FileBeats
- MetricBeats 

These Beats allow us to collect the following information from each machine:

- Filebeat collects data about the file system, which files have changed  and when they changed.

- Metricbeat collects machine metrics, such as uptime.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned:

SSH into the control node and follow the steps below:

- Copy the YAML file to /etc/ansible.

- Update the /etc/ansible/hosts file to include host group, private IP address and the following 'ansible_python_interpreter=/usr/bin/python3'

- Run the playbook, and navigate to curl localhost/setup.php to check that the installation worked as expected.

- The playbooks are listed as install-elk.yml / filebeat-playbook.yml / metricbeat-playbook.yml /ansible_config.yml and are meant to be copied into /etc/ansible directory.

- To make Ansible run the playbook on a specific machine, update the /etc/ansible/hosts file. Within this file, name groups using square brackets (currently contains '[webservers]' and '[elk]') surrounding the group-name and under the group-name, replace private IP's with your own respective IP's. You then use these group-names behind the "hosts:" field in the playbooks to specify which machines to apply the playbook to.

- To check if the ELK server is running, navigate to http://[your.VM.IP]:5601/app/kibana

