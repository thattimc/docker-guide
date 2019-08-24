# Containers and Virtual Machines

Containers and virtual machines have similar resource isolation and allocation benefits but functions differently because containers virtualize the operating system instead of hardware. Containers are more portable and efficient.

![Containers and Virtual Machines](https://raw.githubusercontent.com/timshingyu/docker-guide/master/images/containers-and-virtual-machines.png)

## Containers

Containers are an abstraction at the app layer that packages code and dependencies together. Multiple containers can run on the same machine and share the OS kernel with other containers, each running as isolated processes in userspace. Containers take up less space than VMs (container images are typically tens of MBs in size), can handle more applications and require fewer VMs and Operating systems.

## VIRTUAL MACHINES

Virtual machines (VMs) are an abstraction of physical hardware, turning one server into many servers. The hypervisor allows multiple VMs to run on a single machine. Each VM includes a full copy of an operating system, the application, necessary binaries, and libraries - taking up tens of GBs. VMs can also be slow to boot.