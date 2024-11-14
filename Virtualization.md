The normal way computing is done is to run one OS
The OS is able to perform some operations that can be risky and thus are not able to be performed by normal programs. We say that these operations are run in **Privileged Mode** while normal applications run in **User Mode**.

Virtualization allows us to run multiple privileged operations to run on the same hardware. Essentially this gives us multiple operating systems. This can be done in several different ways
## Software Virtualization
Emulated Virtualization = When the host operating system is the one making privileged mode calls but comes with a **hypervisor**. We can then run virtual machines that have their own operating systems and virtual versions of the physical hardware. These VMs interact with the hypervisor.
	This is good but is very slow

Para-Virtualization = similar to Emulated virtualization but only works on OSs that can be modified. The OSs on the VM is modified so that it makes calls directly to the hypervisor.
## Hardware Virtualization
The cpu can help out the hypervisor
The VM OSs will make calls to the hardware (i.e. cpu) and then the hardware will make calls to the hypervisor.

SR-IOV = a network card feature that makes it appear to VMs that they have their own mini network card. In [[Elastic Compute Cloud|EC2]] this is called Enhanced Networking
