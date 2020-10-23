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

The machines on the internal network are not exposed to the public Internet. The Jumpbox is the only virtual machine that accepts internet connections. Additionally, machines within the network can only be accessed by the Jumpbox. Access policies are controlled within Azure's security groups. Port configurations applied are Deny All Inbound with port 22 exceptions for administration.


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
Now that docker is installed, install the ansible repository and run the container:

```
$ sudo docker pull cyberxsecurity/ansible
$ docker run -ti cyberxsecurity/ansible:latest bash
```
Because Ansible will handle the web applications on each internal machine, an SSH key is required to connect to the machines.
Create a SSH key with default filepath and copy the public key to each virtual machine in Azure:

```
$ ssh-keygen
$ cat ~/.ssh/id_rsa.pub
```
After establishing connections to the web servers, they must be added to ansible's host file:

```
$ nano /etc/ansible/hosts
```
Uncomment [webservers] in located in /etc/ansible/hosts.
Add web server internal IP addresses including the ansible python interpreter path:

```
[webservers]
10.0.0.x ansible_python_interpreter=/usr/bin/python3
10.0.0.x ansible_python_interpreter=/usr/bin/python3
10.0.0.x ansible_python_interpreter=/usr/bin/python3
...
```
Edit the remote username to each web server:

```
nano /etc/ansible/ansible.cfg

remote_user = [username]
```


### Elk Stack Configuration



