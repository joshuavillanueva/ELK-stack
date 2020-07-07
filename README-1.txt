## Automated ELK Stack Deployment

The files in this repository were used to configure the network depicted below.

(Images/diagram(1).jpg)

These files have been tested and used to generate a live ELK deployment on Azure. They can be used to either recreate the entire deployment pictured above. Alternatively, select portions of the playbook file may be used to install only certain pieces of it, such as Filebeat.

  - my-playbook.yml
    ---
      - name: My first playbook
        hosts: webservers
        become: true
        tasks:

        - name: Install apache httpd  (state=present is optional)
          apt:
            name: apache2
            state: present

This document contains the following details:
- Description of the Topology
- Access Policies
- ELK Configuration
  - Beats in Use
  - Machines Being Monitored
- How to Use the Ansible Build


### Description of the Topology

The main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the D*mn Vulnerable Web Application.

Load balancing ensures that the application will be highly responsive, in addition to restricting access to the network.
- Load balancers help eliminate single points of failure and reroutes traffic to another server if one server is compromised by a DDoS attack.
- The Jump Box functions as a gateway that connects directly to the devices on the security zone. It is a secured system that admins have to connect first before accessing the security zone.

Integrating an ELK server allows users to easily monitor the vulnerable VMs for changes to the files and system failures.
- Filebeat monitors specified log files and locations and forwards log events to Elasticsearch for indexing.
- Metricbeat monitors servers by collecting metrics from the system and services running on the server.

The configuration details of each machine may be found below.

| Name     | Function   | IP Address   | Operating System |
| -------- | ---------- | ------------ | ---------------- |
| Jump Box | Gateway    | 52.229.51.21 | Linux            |
| Web-1    | Web server | 10.0.0.5     | Linux            |
| Web-2    | Web server | 10.0.0.6     | Linux            |
| ELK      | ELK server | 10.1.0.4     | GUI              |

### Access Policies

The machines on the internal network are not exposed to the public Internet. 

Only the Jump Box machine can accept connections from the Internet. Access to this machine is only allowed from the following IP addresses:
- 184.96.49.202
- 10.0.0.4

Machines within the network can only be accessed by the Jump Box.
- I allowed only the Jump Box with IP address 52.229.51.21 to access the ELK server. 

A summary of the access policies in place can be found in the table below.

| Name     | Publicly Accessible | Allowed IP Addresses    |
| -------- | ------------------- | ----------------------- |
| Jump Box | Yes                 | 184.96.49.202, 10.0.0.4 |
| Web-1    | No                  | 52.229.51.21            |
| Web-2    | No                  | 52.229.51.21            |
| ELK      | No                  | 52.229.51.21            |

### Elk Configuration

Ansible was used to automate configuration of the ELK machine. No configuration was performed manually, which is advantageous because it lets you quickly and easily deploy multitier apps without having to configure the apps on every machine manually.

The playbook implements the following tasks:
- Install Docker module
- Increase virtual memory to 262144
- install Python3-pip
- Download and launch a docker elk container
- List the ports that ELK runs on 5601, 9200, and 5044

The following screenshot displays the result of running `docker ps` after successfully configuring the ELK instance.

(Images/ansible_to_elk.jpg)

### Target Machines & Beats
This ELK server is configured to monitor the following machines:
- 10.0.0.5 and 10.0.0.6

We have installed the following Beats on these machines:
- Filebeat and Metricbeat

These Beats allow us to collect the following information from each machine:
- Filebeat handles audit logs, depreciation logs, server logs, and slow logs.
- Metricbeat handles system metrics.

### Using the Playbook
In order to use the playbook, you will need to have an Ansible control node already configured. Assuming you have such a control node provisioned: 

SSH into the control node and follow the steps below:
- Copy the filebeat configuration file to the ELK VM.
- Update the filebeat configuration file to include the IP address of the ELK server.
- Run the playbook, and navigate to the filebeat installation page on the ELK server GUI to check that the installation worked as expected.

- Navigate to the ELK's IP address <ELK IP address>:5601/app/kibana to verify if it's running properly.

  (Images/kibana page)
