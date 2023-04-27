# Multipass tools
These are Bash scripts to extend the usability, scripting and automation possiblities of the [Multipass](https://multipass.run/) tool.

Multipass installation is needed:
```
sudo snap install multipass
```
Note that root privileges (sudo) are needed to add a route from host to a VM instance when you want to use [mp-route](#mp-route) tool or set a static IP to the VM using either [mp-ssh](#mp-ssh) or [mp-launch](#mp-launch) with the --ip option.

## Installation

Use the [setup](../README.md#setup) script to install the tools.

## mp-ssh
The **mp-ssh** enables SSH connection to a Multipass instance from the host machine.
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
The **mp-launch** enables creation of a Multipass instance with a static IP address and SSH connection from the host machine without extra manual steps. The tools uses Multipass for launching a VM (Ubuntu LTS by default) and the [mp-ssh](#mp-ssh) tool for enabling SSH connection or adding a static IP to the VM.

### Full usage and options:
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

## mp-route
The **mp-route** adds, changes or deletes a peristent route to Multipass instance. The routes are persisted by using oneshot [systemd](https://systemd.io/) services which are enabled and autostarted on reboot of the host. 

The [mp-ssh](#mp-ssh) tool is using this script when it creates a route from a host machine to a virtual machine with a static IP address. Superuser privileges (or 'sudo' rights) are needed for creating the routes and systemd services by the tool.

The tool uses the [persistent-route.service](persistent-route.service) template file for creating and starting a new systemd service. The created new unit file is placed in /etc/systemd/system/ and the service is started and enabled to be autostarted on reboot.

### Full usage and options:
```
mp-route -h
```

### Example
Remove a systemd service enabling a route from host to the VM named 'my-vm' created with either of the tools in the above examples:
```
mp-route -d my-vm
```
The systemd service unit will be disabled, stopped and removed, but the route itself is not automatically deleted until the host or its network is restarted. But the script will display a command in the terminal which can be used to manually remove the route.

## mp-delete
The **mp-delete** deletes Multipass instances created or configured with or without the [mp-ssh](#mp-ssh) tool (or with any tool which is using the mp-ssh, like [mp-launch](#mp-launch)).

The tool also deletes any services created for the deleted instances by the [mp-route](#mp-route) (but superuser privileges are needed to remove the services). The known hosts keys set by [mp-ssh](#mp-ssh) tool (to enable promptless SSH connection from host to the VM) are also removed.

### Full usage and options:
```
mp-delete -h
```

### Examples
Delete the VM instance named 'my-vm', to be purged with the `mp-delete --purge my-vm` (or with the `multipass purge`) command:
```
mp-delete my-vm
```
The above command will delete the VM instance but will not purge all its data, so you could recover the VM instance:
```
multipass recover my-vm
```
Delete and purge the VM instances named 'my-vm' and 'test-vm' and all their data immediately:
```
mp-delete -p my-vm test-vm
```
Delete and purge all VM instances configured with the [mp-ssh](#mp-ssh) or created with the [mp-launch](#mp-launch) (or any tool using those tools):
```
mp-delete -p --all
```
