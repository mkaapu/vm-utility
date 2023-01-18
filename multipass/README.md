# Multipass tools
These are Bash scripts to extend the usability, scripting and automation possiblities of the [Multipass](https://multipass.run/) tool.

Multipass installation is needed:
```
sudo snap install multipass
```

## Installation

Use the simple setup script from the root of the repository to copy tools to /usr/bin/local where they are available for all users and other tools:
So, to clone and install the tools:
```
git clone https://github.com/mkaapu/vm-utility.git
sudo vm-utility/setup
```
Or you can just clone the project and add the multipass directory to your PATH.

## mp-ssh
Enables SSH connection to a Multipass instance from host machine.
It can be used to set a static IP address to multipass instance.

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
Enables creation of Multipass instance with a static IP address and SSH connection from host machine without extra manual steps.

## Full usage and options:
```
mp-launch -h
```
Or read [mp-launch-usage](https://github.com/mkaapu/vm-utility/blob/main/multipass/mp-launch-usage).

### Example
Create a new Ubuntu LTS VM with a static IP address and enable acccess to the VM instance from host machine through SSH:
```
mp-launch --name my-vm --ip 10.10.10.10
ssh ubuntu@10.10.10.10
```

