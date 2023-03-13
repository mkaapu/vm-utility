# vm-utility
This repository is just a collection of VM launch and configuration utility tools for scripting and automation.
Scripts are written in Bash and tested on Ubuntu Linux distributions.
Note that some of the tools need to be exectuted either with superuser privileges or as root user to complete some administrative commands.

## Setup
The setup script will copy vm-utility tools to */usr/bin/local* so they will be available for all users and other tools. 

To clone and install tools, run:
```
git clone https://github.com/mkaapu/vm-utility.git
sudo vm-utility/setup
```
The setup tool can be executed more interactively with -i option which allows prompt before owerwriting any existing files.

## Tools to enhance Multipass
The **multipass** directory contains bash scripts to extend the usability, scripting and automation possiblities of the [Multipass](https://multipass.run/) tool.

### mp-ssh
- Enables SSH connection to a Multipass instance from the host machine.
- Can be used to set a static IP address to a multipass instance.
- Provides a minimal interface suitable for use by other shell scripts and automation tools.
- [Documentation](multipass#mp-ssh)

### mp-lauch
- Enables creation of a Multipass instance with a static IP address and SSH connection from the host machine without extra manual steps.
- Provides a minimal interface suitable for use by other shell scripts and automation tools.
- [Documentation](multipass#mp-launch)

## Tools to setup Jenkins CI with VMs
The **jenkins** directory contains bash scripts to help to setup [Jenkins](https://www.jenkins.io/) CI with controller isolation and distributed build agents based on virtual machines.

### launch-vm-jenkins
- Creates a Ubuntu LTS VM and prepares it as a Jenkins server.
- Installs Docker to the VM
- Runs a Docker in Docker container in order to execute Docker commands inside Jenkins nodes on the VM
- Runs a Docker container hosting a Jenkins controller with Blue Ocean plugins and features on the VM
- Enables logging into the VM using SSH tunnel through a local port of the host.
- [Documentation](jenkins/vm-controller#launch-vm-jenkins)

### launch-vm-agent
- Creates a Ubuntu LTS VM and prepares it as a Jenkis agent.
- Installs Java JDK 17 to the VM.
- Enables logging into the VM using SSH tunnel through a local port of the host.
- [Documentation](jenkins/vm-agent#launch-vm-agent)

## Tools to enable remote login with SSH
The **ssh** directory contains bash scripts to enable automated remote login and command-line execution of SSH application.

### make-ssh-tunnel
- Creates a persistent SSH tunnel between servers as systemd service.
- [Documentation](ssh#make-ssh-tunnel)

### rm-ssh-tunnel
- Removes a SSH tunnel and systemd service created by the [make-ssh-tunnel](#make-ssh-tunnel)
- [Documentation](ssh#rm-ssh-tunnel)
