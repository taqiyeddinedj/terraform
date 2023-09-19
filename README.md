# Terraform & Docker Nginx Deployment
This repository contains Ansible and Terraform code to automate the deployment of an Nginx web server in a Docker container.

## Prerequisites
1. Ubuntu 20.04
2. Ansible installed
3. Terraform installed (or will be installed through the Ansible playbook)
4. Docker installed

    ```
    sudo apt-get update
    sudo apt-get install docker.io
    ````

## Overview
The Ansible playbook takes care of:

* Updating the package cache
* Setting up the necessary repositories and keys for Terraform
* Installing the required packages including Docker and Terraform
* Adding the executing user to the Docker group for permissions
* Cloning the Terraform configurations from this repository
* Initializing and applying the Terraform configurations

The Terraform configuration takes care of:

* Pulling the latest Nginx Docker image
* Creating a Docker container from the Nginx image with port 80 mapped to host's port 8080
* Mounting a local directory to the Nginx's HTML directory for serving web content
## Usage
1. Clone this repository:

```
git clone https://github.com/taqiyeddinedj/terraform.git
cd terraform
```

2. Run the Ansible playbook:

``ansible-playbook deploy-web.yml``

## Customizations
### Home Directory
The playbook and Terraform configuration uses the home directory of the user executing the commands.
In my case i have a user with ahome directory called 'ubuntu' for taht you have to change the host path inside main.tf in the volume section.

### Docker Image
 You can change the docker_image resource in main.tf to use a different Docker image or version.

3. Check your Nginx web server:
After the playbook completes successfully, you can open a browser and navigate to http://<your_server_ip>:8080 to see your Nginx welcome page.