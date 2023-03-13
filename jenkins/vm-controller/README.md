# launch-vm-jenkins
The **launch-vm-jenkins** tool creates an [Ubuntu](https://ubuntu.com/) LTS virtual machine and sets up and hosts a [Jenkins](https://www.jenkins.io/) controller as a [Docker](https://www.docker.com/) container on the VM.
Two containers are set up to run in the VM, one hosting the Jenkins server and other hosting the Docker daemon, so that Docker CLI is usable inside the Jenkins container.
Jenkins controller is installed with Blue Ocean plugins and features.

Jenkins setup on the VM is mostly automation based on the instructions given on https://www.jenkins.io/doc/book/installing/docker/#downloading-and-running-jenkins-in-docker.

## Installation
The tool has dependencies on the other tools in the *vm-utility* repository, so easiest way is to install them using the setup script from the root of the repository.
To setup all the tools to /usr/local/bin:
```
sudo ./setup
```

## What it does
* **launch-vm-jenkins** utility installs [Multipass](https://multipass.run/) tool if it is not installed (needs sudo permissions).
* It generates a new SSH key if no existing key (ed25519) is found from user's home directory (*.ssh/id_ed25519*).
* It creates an Ubuntu LTS virtual machine with the settings specified by given commandline options.
* It stores the public SSH key of the host to the authorized_keys file on the VM to allow passwordless login with public key authentication.
* It sets a static IP address to the VM (specified by the --vm-ip option).
* The *.ssh/known_hosts* in user's home directory is appended with the VM's host key to enable promptless SSH connection to the VM.
* vm-utility tools are installed to the VM.
* Docker is installed and set up on the VM and the default 'ubuntu' user is added to the Docker group.
* The docker:dind Docker image is downloaded and run inside the VM as container in order to execute Docker commands inside Jenkins nodes.
* The official Jenkins Docker image is built with a customized Dockerfile enabling the "blueocean docker-workflow" plugins.
* The customized image is run as a container in Docker to initialize and host the Jenkins controller.
* The further instructions for inital setup of Jenkins server are povided on the terminal.
* Local port of the host (--port option with default value 8080) is forwarded to a port on VM (--jenkins-port, default 8080) for accessing Jenkins.
* The persistent SSH tunnel is created with a systemd service that enables accessing Jenkins GUI through the host's port.

## Full usage and options
```
launch-vm-jenkins -h
```
## Example
Launch a Jenkins controller on a virtual machine:
```
launch-vm-jenkins --name jenkins-controller --cpus 2 --mem 8G --disk 100G --host-ip 10.101.123.111 --vm-ip 10.100.123.101 --port 8888 --tag latest-jdk17 jenkins-vm
```
With this example:
* New Ubuntu LTS VM will be launched with the name 'jenkins-vm'.
* 2 CPUs, 8G of memory and 100G of disk space will be allocated to the launched VM.
* The virtual machine will have static IP: 10.100.123.101
* The host (where you execute the above command) should have an IP address: 10.101.123.111 (binding the Jenkins port 8888 to that address)
* The new Jenkins server will be set up on the VM inside the Docker container with the name 'jenkins-controller'
* The new Jenkins controller should be accessible at http://10.101.123.111:8888/
* The Jenkins core installation should be based on the image with the *jenkins/jenkins:latest-jdk17* tag on the Docker Hub.
