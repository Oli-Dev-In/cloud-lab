# Port Forwarding

## What is it and what problem does it solve

Port forwarding solves the problem of reaching a service running inside a 
NAT network from the outside. In NAT mode, the VM is hidden behind 
VirtualBox and Windows cannot reach it directly. Port forwarding tells 
VirtualBox: "when a connection arrives on this port on Windows, redirect 
it to this port on the VM."

This works the same way locally and on remote servers — the principle is 
identical whether you are connecting to a local VM or an AWS EC2 instance 
behind a firewall.

## How it works — our SSH example

A request arriving on Windows port 2222 is automatically redirected to 
port 22 on the VM — where the OpenSSH server is listening.

| Field | Value | Meaning |
|---|---|---|
| Host IP | 127.0.0.1 | Windows — the machine initiating the connection |
| Host Port | 2222 | Port on Windows that receives the connection — 2222 chosen to avoid conflicts if port 22 is already in use on Windows |
| Guest IP | 10.0.2.15 | The VM — the destination of the redirected connection |
| Guest Port | 22 | Standard SSH port on the VM where OpenSSH server listens |

## Real world usage

### Local VM
Connecting to ubuntu-server-01 in VirtualBox from VSCode terminal — 
VirtualBox redirects the connection from Windows port 2222 to VM port 22.

### Cloud — AWS EC2
On AWS, security groups play a similar role — they control which ports are 
open and accessible from the outside. Port 22 is opened in the security 
group to allow SSH connections to EC2 instances.