# Multipass tools
These are Bash scripts to extend the usability, scripting and automation possiblities of the [Multipass](https://multipass.run/) tool.

Multipass installation is needed:
```
$ sudo snap install multipass
```

## Installation
Just clone the project. 
Keep the files in the same directory.
You may want to add the directory to your PATH (or copy the directory to /usr/local/bin on Ubuntu) if you want make the tools more available.

## mp-ssh
Enables SSH connection to a Multipass instance from host machine.
It can be used to set a static IP address to multipass instance.

### Full usage and options:
```
./mp-ssh -h
```

### Example
Set a static IP address to a multipass instance:
```
$ multipass launch --name my-vm
$ ./mp-ssh --ip 10.10.10.10 my-vm
$ ssh ubuntu@10.10.10.10
```

## mp-launch
Enables creation of Multipass instance with a static IP address and SSH connection from host machine without extra manual steps.

## Full usage and options:
```
./mp-launch -h
```
OR
read [usage](https://github.com/mkaapu/vm-utility/blob/main/multipass/usage).

### Example
Create a new Ubuntu LTS VM with a static IP address and enable acccess to the VM instance from host machine through SSH:
```
$ ./mp-launch --name my-vm --ip 10.10.10.10
$ ssh ubuntu@10.10.10.10
```

