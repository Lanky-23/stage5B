# NestJS Boilerplate Deployment with Ansible

This project provides an Ansible playbook for deploying a NestJS boilerplate application with PostgreSQL, RabbitMQ, and Nginx.

## Prerequisites

- Ansible installed on the control machine
- SSH access to the target host(s)
- Git installed on the control machine

## Setup

Generate an SSH key pair:
```sh
ssh-keygen
```
Install Ansible:
```  
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository --yes --update ppa:ansible/ansible
sudo apt install ansible -y
```
Clone the repository:
```
git clone https://github.com/Rob-in-son/hng_boilerplate_nestjs.git
cd hng_boilerplate_nestjs
git checkout devops
cd ansible
```
Configure the inventory file (inventory.yml):
```
all:
  hosts:
    <host_name>:
      ansible_host: <host_ip>
      ansible_user: <username>
      ansible_ssh_private_key_file: <private_key_path>
```
### Playbook Structure
- main.yml: Main playbook
- nginx.conf.j2: Nginx configuration template
- nestjs.service.j2: Systemd service template
### Deployment
```
ansible-playbook main.yml -i inventory.yml -v
```
### What the Playbook Does
- Sets up a new user for the application
- Installs dependencies (Node.js, PostgreSQL, Nginx, RabbitMQ)
- Clones the repository
- Configures PostgreSQL
- Sets up the environment
- Configures Nginx as a reverse proxy
- Configures UFW firewall
- Sets up the application as a systemd service
- Configuration
- Variables in main.yml:

