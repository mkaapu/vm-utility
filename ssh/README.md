# SSH Tools

These are Bash scripts to enable automated remote login and command-line execution of SSH applications.

## Installation

Use the simple setup script from the root of the repository to copy tools to */usr/bin/local* where they are available for all users and other tools:
```
git clone https://github.com/mkaapu/vm-utility.git
sudo vm-utility/setup
```
Or you can just clone the project and add the *ssh* directory to your PATH.

## make-ssh-tunnel
Creates a persistent SSH tunnel between servers with systemd.

### What it does
* **make-ssh-tunnel** creates a systemd service which enables persistent SSH tunnel from a local port to a port on an external server.
* Uses the *ssh-tunnel-persistent.service* template file for writing the systemd unit file to *~/.config/systemd/user/*.
* Starts the service and enables the service to be autostarted.
* Enables the user process for the service to run without any open sessions on the local host.
* When connection is dropped, then systemd will wait 3 seconds and continuously attempt to reconnect.

### Full usage and options
```
make-ssh-tunnel -h
```

### Example
```
make-ssh-tunnel --bind 10.10.10.10 --port 3333 --ip 11.11.11.11 --to-port 333 --user ubuntu vmserver
```
* Creates a persistent SSH tunnel from local port 3333 on host with IP address 10.10.10.10 to port 333 on external server with IP address 11.11.11.11.
* Writes a systemd user unit file with the path *~/.config/systemd/user/ssh-tunnel-from-3333-to-vmserver.service*
* Starts the *ssh-tunnel-from-3333-to-vmserver.service* and enables automatic start-up of the service.

## rm-ssh-tunnel
Removes a persistent SSH tunnel between servers created by the [make-ssh-tunnel](#make-ssh-tunnel).
It stops and removes the systemd service and related user unit files.

To remove the SSH tunnel and the service created by the above [example](#example):
```
rm-ssh-tunnel --port 3333 vmserver
```

### Full usage and options
```
rm-ssh-tunnel -h
```
