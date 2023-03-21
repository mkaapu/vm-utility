# Multipass tools
These are Bash scripts to extend the usability, scripting and automation possiblities of the [Multipass](https://multipass.run/) tool.

Multipass installation is needed:
```
sudo snap install multipass
```
Note that root privileges (sudo) is needed to add a route from host to a VM instance when you want to set a static IP to the VM using either mp-ssh or mp-launch with -i option.

## Installation

Use the [setup](../README.md#setup) script to install the tools.

## mp-ssh
Enables SSH connection to a Multipass instance from the host machine.
It can be used to set a static IP address to a multipass instance.

### Full usage and options:
```
mp-ssh -h
```

### Example
Set a static IP address to a multipass instance:
```
multipass launch --name my-vm
mp-ssh --ip 10.10.10.10 my-vm
ssh ubuntu@10.10.10.10
```

## mp-launch
Enables creation of a Multipass instance with a static IP address and SSH connection from the host machine without extra manual steps.

## Full usage and options:
```
mp-launch -h
```
Or read [mp-launch-usage](mp-launch-usage).

### Example
Create a new Ubuntu LTS VM with a static IP address and enable acccess to the VM instance from the host machine through SSH:
```
mp-launch --name my-vm --ip 10.10.10.10
ssh ubuntu@10.10.10.10
```

