# Virtualization

## What is it and what problem does it solve

Virtualization allows a physical machine to allocate part of its capacity to one or more virtual machines. It solves the problem of servers being used at only a fraction of their total capacity. Instead of wasting resources, multiple virtual machines can run on the same physical hardware simultaneously.

## Key vocabulary

### Host
The physical machine that provides the real hardware — CPU, RAM, storage. In my case: my Windows PC.

### Guest
The virtual machine (VM) running inside the host. It thinks it is a real independent computer but shares the host's hardware. In my case: Ubuntu Server.

### Hypervisor
The software that sits between the host and the guests. It manages resource allocation — how much CPU and RAM each VM receives. There are two types:

### Type 1 — Bare Metal
Runs directly on physical hardware with no OS underneath. More performant and efficient. Used in professional datacenters.
Examples: AWS Nitro, VMware ESXi, Microsoft Hyper-V

### Type 2 — Hosted
Runs on top of an existing operating system. Less performant than Type 1 but perfect for learning and development on a personal computer.
Examples: VirtualBox (what I use), VMware Workstation

## Why Ubuntu Server

1. Most widely used Linux distribution on AWS EC2 instances — learning on Ubuntu means learning in the same conditions as production.
2. No graphical interface — terminal only. A cloud engineer works in the terminal, not with a mouse. Better to learn correctly from the start.
3. Large community and documentation — any problem I encounter has already been solved and documented online.