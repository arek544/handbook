## Containers vs Virtual Machines

`#container` `#docker` `#VM` `#virtual` `#explained`

### TL;DR

Docker containers **share resources with your host operating system**, and this is done by the Docker Daemon; a Virtual Machine doesn’t

## Advantages

- fast start-up
- low resources consumption (CPU, RAM, ROM)

### A virtual machine:

- runs a full-blown guest operating system with virtual access to host resources through a Hypervisor.
- Now in general VMs provide an environment with more resources than most applications need.

### Container: 

- runs natively on Linux and shares the kernel of the host machine with other containers.
- It runs a discreet process and because it doesn’t take any more memory than other executables, it’s **lightweight**.

## Explanation by analogy
- **VM** - is like a house, have their own infrastructure, plumbing, heating, and electrics
- **Docker** - is like a apartment, shares plumbing, heating, and electrics
