# ISO Disk Image

## What is it
An ISO is the virtual equivalent of a physical installation DVD. It is a bit-for-bit copy of an installation disc — all the content, in the correct order, ready to be used as if it were a real physical disc.

## What problem does it solve
A VM without an operating system is an empty shell — it cannot do anything. An ISO provides the installation media that allows an OS to be installed on the VM, making it functional.

## Real world usage

### Virtual Machines
When creating a VM in VirtualBox, you provide the hypervisor with an ISO file. The hypervisor mounts it as a virtual DVD drive. The VM boots from it and installs the operating system — exactly like a physical computer booting from a DVD.

### Cloud — AWS AMI
In AWS, the equivalent of an ISO is called an AMI — Amazon Machine Image. When AWS creates a new EC2 instance, it boots from an AMI, which is a complete image of a system ready to run. Same concept, different name, adapted for cloud scale.