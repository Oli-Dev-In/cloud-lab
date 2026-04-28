# SSH — Secure Shell

## What is it and what problem does it solve

SSH is a protocol that allows secure, encrypted connection to any Linux server over a network — whether local or on the other side of the world. It solves the problem of remote server access: without SSH, you would need to be physically in front of every server you manage. With SSH, you connect from your terminal and work on the remote server exactly as if you were sitting in front of it.

## Client / Server model

SSH works with two components:

**SSH client** — the software that initiates the connection. Already installed by default on Windows 10/11. Used from the VSCode terminal to connect to any server.

**SSH server** — the software running on the target server, waiting for incoming connections. In our case: OpenSSH server, installed during Ubuntu Server setup. Without it, no connection is possible.

This is a client-server model — a universal concept in computing that appears everywhere in cloud and DevOps work.

## Real world usage

### Local VM
Connecting to ubuntu-server-01 running in VirtualBox from the VSCode terminal on Windows — instead of using the VirtualBox window directly. Enables copy-paste, comfortable workflow, professional environment.

### Cloud — AWS EC2
When an EC2 instance is running on AWS in a datacenter in Dublin or Frankfurt, SSH is the standard way to connect and manage it. You never interact with cloud servers through a graphical interface — always through SSH from your terminal.