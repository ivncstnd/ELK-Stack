## Automated ELK Stack Deployment Project
Files used in this repository were used to create and configure the network below.

(network_diagram)

This document discusses the following:
- Description of the Toplogy
- Access Policies
- Ansible Usage
- ELK Stack Configurations
  - Virtual machines monitoring
  - Configuring Beats

### Discription of the Toplogy

The toplogy was built using Microsoft's Azure Cloud services. With given computational tools, the main purpose of this network is to expose a load-balanced and monitored instance of DVWA, the Damn Vulnerable Web Application. 

By using load-balancing solutions, security is better insured through fault tolerance and redudancy. In addition, the ability to restrict and control access through network segementation increases overall hardening.

Integrating an ELK server allows users to easily monitor the vulernable VMs for changes to the logs and system resources.

The configuration details of each machine can be found below.

| Name    | Function | IP Address | Operating System |
|---------|----------|------------|------------------|
| Jumpbox | Gateway  | 10.0.0.4   | Ubuntu 18.04-LTS |
| Web-1   | DVWA     | 10.0.0.5   | Ubuntu 18.04-LTS |
| Web-2   | DVWA     | 10.0.0.6   | Ubuntu 18.04-LTS |
| Web-3   | DVWA     | 10.0.0.7   | Ubuntu 18.04-LTS |
| ELK-1   | Monitor  | 10.1.0.4   | Ubuntu 18.04-LTS |

### Access Policies

The machines on the internal network are not exposed to the public Internet. The Jumpbox is the only virtual machine that accepts internet connections. Additionally, machines within the network can only be accessed by the Jumpbox. 


### Ansible Usage

To utilize Ansible and Ansible playbooks, the Docker engine needs to be installed within the Jumpbox. 
Within the Jumpbox enviroment, update and install docker:

```
$ sudo apt-get update
$ sudo apt-get upgrade
$ sudo apt install docker.io
```

After the installation, check and enable docker on the system:

```
$ sudo systemctl start docker
$ sudo systemctl enable docker
```


### Elk Stack Configuration



