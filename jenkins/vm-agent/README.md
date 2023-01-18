# launch-vm-agent
Tool to create a Ubuntu LTS VM and prepare it as a [Jenkins](https://www.jenkins.io/) agent.

## What it does
* **launc-vm-agent** utility installs [Multipass](https://multipass.run/) tool if it is not installed.
* It generates a new SSH key if no existing key (ed25519) is found from user's home directory (*.ssh/id_ed25519*).
* It creates a Ubuntu LTS virtual machine with the settings specified by given commandline options.
* It stores the public SSH key of the host to the authorized_keys file on the VM to allow passwordless login with public key authentication.
* It sets a static IP address to the VM (specified by the -v option).
* The *.ssh/known_hosts* in user's home directory is appended with the VM's host key to enable promptless SSH connection to the VM.
* Java OpenJDK 17 is installed on the VM to make it possible to launch Jenkins agents there.
* Local port of the host (defaults to 2222 but can be specified with the -p option) is forwarded to the VM to enable SSH tunneling.
* The SSH tunnel is enabled on startup with the host's crontab to enable launching Jenkins agents on the VM through the host's port.

## Full usage and options
```
launch-vm-agent -h
```
## Example
Prepare VM as a Jenkins agent:
```
launch-vm-agent --name vm-agent --cpus 2 --mem 2G --disk 10G --host-ip 10.101.123.111 --vm-ip 10.100.123.101 --port 3333
```
With this example:
* New Ubuntu LTS VM will be launched with the name 'vm-agent'.
* 2 CPUs, 2G of memory and 10G of disk space will be allocated to the launched VM.
* VM will have static IP: 10.100.123.101
* The host (where you execute the above command) should have an IP address: 10.101.123.111
* You should be able to log in to the VM through the local port of the host: 3333

You can log directly in to the VM launched in the above example using SSH:
```
ssh ubuntu@10.100.123.101
```
of through the local port of the host:
```
ssh -p 2222 ubuntu@10.101.123.111
```
If you connect through the local port you are prompted whether you want to add the VM to known hosts. To silence that for instance in scripts:
```
sh-keyscan -H -t ed25519 -T 30 -p 3333 10.101.123.111 >> ~/.ssh/known_hosts
ssh -p 3333 ubuntu@10.101.123.111
```
