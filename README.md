# NestJS Boilerplate Deployment with Ansible

This repository provides an Ansible playbook to automate the deployment of a NestJS boilerplate application. It includes the setup for Node.js, PostgreSQL, RabbitMQ, Nginx, and configuration of the application environment.

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

### Usage
Edit the Inventory File: Update the inventory file (hosts) with your server details.
Run the Playbook: Execute the playbook using the following command:
```
ansible-playbook -i hosts deploy_nestjs_boilerplate.yml
```
Verify Deployment: After running the playbook, verify the following:

- The NestJS application is running and accessible through Nginx.
- PostgreSQL and RabbitMQ are configured properly.
- Logs are being generated as expected in the /var/log/stage_5b directory.
  
### Configuration
You may need to adjust the following variables in the playbook to fit your environment:

- app_dir: Directory where the application will be deployed.
- rabbitmq_password: Password for RabbitMQ default user.
- log_dir: Directory for application logs.
- app_user: User under which the application will run.
- db_name, db_user, db_password: PostgreSQL database credentials.
- profile, node_env, port: Application environment settings.
- db_host, db_port, db_entities, db_migrations, db_type, db_ssl: Database - connection settings.
- jwt_secret, jwt_expiry_timeframe: JWT settings.

### Troubleshooting
- Permissions Issues: Ensure the hng user has appropriate permissions for the application directory and log files.
- Service Failures: Check the status of services (Nginx, RabbitMQ, etc.) using systemctl status <service>.
