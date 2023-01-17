# vm-utility
This repository is just a collection of VM launch and configuration utility tools for scripting and automation.
Scripts are written with Bash and tested on Ubuntu Linux distributions.

## Setup
The setup script will copy vm-utility tools to */usr/bin/local* so they will be available for all users and other tools (although some scripts needs superuser privilidges to execute). So to clone and setup tools, run:
```
git clone https://github.com/mkaapu/vm-utility.git
vm-utility/setup
```
The setup tool has also interactive mode with -i option which will prompt before owerwriting any existing files.

## mp-tools for multipass (multipass directory)
The **multipass** directory contans bash scripts to extend the usability, scripting and automation possiblities of the [Multipass](https://multipass.run/) tool.

### mp-ssh
- Enables SSH connection to a Multipass instance from host machine.
- Can be used to set a static IP address to multipass instance.
- Provides a minimal interface suitable for use by other shell scripts and automation tools.

### mp-lauch
- Enables creation of Multipass instance with a static IP address and SSH connection from host machine without extra manual steps.
- Provides a minimal interface suitable for use by other shell scripts and automation tools.
