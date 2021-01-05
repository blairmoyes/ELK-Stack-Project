## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

![](https://user-images.githubusercontent.com/66808028/101435841-478e7600-38ca-11eb-98f0-650b335db6e5.png)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, the filebeat-playbook.yml and metricbeat-playbook.yml files may be used to install only certain pieces of it, such as Filebeat or Metricbeat, respectively.

  - install-elk.yml
  - filebeat-playbook.yml
  - metricbeat-playbook.yml

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
- Load balancers protect the availablity of a network. 
- A jump box provides a highly secure gateway router from which we can administer our other VMs. Placing a gateway between the internet and the rest of the network forces all traffic through a single node. This drastically reduces the surface area of attack on the network.


Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the logs and system files.
- Filebeat monitors information about the file systems, including which files have changed and when. It is often used to monitor changes in very specific files.
- Metricbeat records statistics about systems and services running on the webservers.

The configuration details of each machine may be found below.

| Name      | Function       | IP Address              | Operating System           |
|-----------|----------------|-------------------------|----------------------------|
| Jump Box  | Gateway        | 10.0.0.4, 40.118.239.56 | Linux Ubuntu Server 18.04  |
| Web-1     | Web Server     | 10.0.0.5                | Linux Ubuntu Server 18.04  |
| Web-2     | Web Server     | 10.0.0.7                | Linux Ubuntu Server 18.04  |
| Web-3     | Web Server     | 10.0.0.8                | Linux Ubuntu Server 18.04  |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from your development machine IP.

Machines within the network can only be accessed by the Jump Box (10.0.0.4).

A summary of the access policies in place can be found in the table below.

| Name      | Publicly Accessible | Allowed IP Addresses                   |
|-----------|---------------------|----------------------------------------|
| Jump Box  | Yes                 | Development Machine IP                 |
| Web-1 VM  | No                  | 10.0.0.4                               |
| Web-2 VM  | No                  | 10.0.0.4                               |
| Web-3 VM  | No                  | 10.0.0.4                               |


### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it ensures that our configurations run identically everywhere, thus eliminating variability.

The install-elk.yml playbook implements the following tasks:
- Install Docker
- Install Python3-pip
- Install Docker module
- Increase maximum virtual memory usage
- Download and launch a Docker ELK container

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

https://user-images.githubusercontent.com/66808028/101436317-2bd79f80-38cb-11eb-9877-41cb8469fa3a.png

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 (Web-1)
- 10.0.0.7 (Web-2)
- 10.0.0.8 (Web-3)

We have installed the following Beats on these machines:
- Filebeat
- Metric Beat

These Beats allow us to collect the following information from each machine:
- Filebeat collects log files and information about the file system, which we use to track usage patterns, changes to file systems, etc. 
- Metric Beat collects statistics the systems and services running on the server, which we use to 

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the install-elk.yml file to /etc/ansible/files.
- Update the /etc/ansible/hosts file to include ELK-Server and Web VM IPs. This will tell Ansible which machines to run the playbook on. List the ELK-Server and Web VMs under separate hostnames. Be sure to point the ELK installation playbook at the ELK-Server and Filebeat & Metric Beat installation playbooks at the Web VMs.
- Run the playbooks, and navigate to http://<ELK-Server Public IP>:5601/app/kibana to check that the installation worked as expected. 

If the ELK installation completed successfully, you'll see the output below.

![](https://user-images.githubusercontent.com/66808028/101436522-912b9080-38cb-11eb-8f0b-4c62bba21f4d.png)

If the Filebeat installation completed succesfully, you'll see this output when you click "Check Data" under Kibana Homepage > Add Log Data > System Logs > DEB Tab > Module Status.

![](https://user-images.githubusercontent.com/66808028/101436921-5544fb00-38cc-11eb-9175-03afc027edf8.png)

If the Metric Beat installation completed succesfully, you'll see this output when you click "Check Data" under Kibana Homepage > Add Metric Data > Docker Metrics > DEB Tab > Module Status.

![](https://user-images.githubusercontent.com/66808028/101436985-7dccf500-38cc-11eb-87c6-f5168e41a1b7.png)

