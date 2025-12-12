# Windows Server Lab Setup (KVM + Spice + Virt-Manager)

## Overview
This document describes the setup of a Windows Server lab running on a Linux host using KVM/QEMU. It serves as the base environment for practicing Acronis Cloud Frontline troubleshooting scenarios.

## Host Environment
- OS: Ubuntu Linux
- Hypervisor: KVM/QEMU
- Management: virt-manager
- Display: SPICE + QXL
- Networking: NAT

## Steps Performed
1. Verified CPU virtualization support: `egrep -c '(vmx|svm)' /proc/cpuinfo`
2. Installed virtualization tools: `sudo apt install qemu-kvm libvirt-daemon-system virt-manager`
3. Created VM with:
   - Windows Server ISO
   - 2 vCPUs, 4–8 GB RAM
   - 40–60 GB disk (qcow2)
   - SPICE display + QXL video
4. Installed Spice Guest Tools for clipboard and resolution integration.
5. Verified network connectivity:
   - `ping 8.8.8.8`
   - `curl -v https://google.com`

## Result
The VM is fully operational and ready for Acronis agent installation and troubleshooting exercises.
