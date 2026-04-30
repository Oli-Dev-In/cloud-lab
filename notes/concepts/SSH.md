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

## Reconnecting after a session

The SSH terminal does not persist between VSCode sessions. Every time you reopen VSCode, you need to reconnect manually.

**Prerequisites**: Ubuntu VM must be running in VirtualBox before connecting.

**Command to reconnect from VSCode terminal:**

```bash
ssh -p 2222 olivier@127.0.0.1
```

**Command breakdown:**

| Element | Meaning |
|---|---|
| `ssh` | The SSH client command |
| `-p 2222` | Connect on port 2222 — required because VirtualBox port forwarding redirects Windows port 2222 to VM port 22. Without `-p`, SSH would try port 22 on Windows directly and fail. |
| `olivier@` | Username to connect with on the remote server. Format is always `user@address`. On AWS you will see `ubuntu@address` or `ec2-user@address` depending on the OS. |
| `127.0.0.1` | Loopback address — always refers to your own local machine. Fixed and universal, never changes. Used here because the VM is hidden behind VirtualBox NAT. On a real AWS server you would use its public IP instead, e.g. `54.123.45.67`. |

Enter your password when prompted. You will land directly in your Ubuntu Server terminal.