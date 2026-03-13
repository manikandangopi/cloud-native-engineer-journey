# Day 01 – Linux Server Provisioning 🐧

![Linux](https://img.shields.io/badge/OS-Linux-blue)
![Ubuntu](https://img.shields.io/badge/Distro-Ubuntu-orange)
![Rocky](https://img.shields.io/badge/Distro-Rocky%20Linux-green)
![VirtualBox](https://img.shields.io/badge/Virtualization-VirtualBox-purple)
![Status](https://img.shields.io/badge/Lab%20Status-Completed-brightgreen)

---

# Objective

The objective of Day 1 was to **build a Linux server lab environment** and understand the **fundamental components required to operate Linux in production systems**.

Tasks performed:

- Setting up virtualization
- Installing Linux operating systems
- Configuring network connectivity
- Configuring system hostname
- Synchronizing system time
- Enabling secure SSH access
- Managing servers remotely via VS Code

---

# Lab Architecture

    Host Machine (Windows)
             │
             │
       VirtualBox Hypervisor
       ┌───────────────┐
       │               │
       │               │

       Ubuntu Server 
       VM Rocky Linux VM
dev-k8s-ubuntulinux-01
dev-k8s-rockylinux-01
10.90.121.74 
10.90.121.214
│ │
└──── SSH Remote Access ────┘
│
VS Code Remote SSH


---

---

# Linux Fundamentals

## What is Linux?

Linux is an **open-source Unix-like operating system family** built around the **Linux kernel**.


Linux = Kernel + GNU Tools


Creator:


Linus Torvalds
Year: 1991


---

# What is an Operating System?

An **Operating System (OS)** manages hardware and software resources.

Responsibilities:

- CPU management
- Memory management
- Disk and filesystem
- Device management
- User and security management

Examples:

- Linux
- Windows
- macOS
- Unix

---

# What is Kernel?

The **Kernel is the core component of the operating system**.

It interacts directly with hardware.

| Area | Kernel Role |
|-----|-------------|
CPU | Process scheduling |
Memory | RAM management |
Disk | Block device management |
Network | TCP/IP networking |
Devices | Hardware drivers |

Kernel **does not provide user commands** such as:

- `ls`
- `cp`
- `bash`

These are **user space tools**.

---

# Kernel Features Used in Containers

| Feature | Purpose |
|------|------|
Namespaces | Container isolation |
Cgroups | CPU & memory limits |
OverlayFS | Container filesystem |
Network stack | Container networking |

---

# Linux Boot Process

Boot flow:


Power ON
↓
BIOS / UEFI
↓
Bootloader (GRUB)
↓
Linux Kernel
↓
Initramfs
↓
systemd
↓
System Services
↓
Login Shell


Explanation:

| Stage | Role |
|------|------|
BIOS | Hardware check |
GRUB | Loads OS |
Kernel | Initializes hardware |
Initramfs | Loads drivers |
systemd | Starts services |
Login | User login |

---

# Linux Distributions

Linux Distribution:


Linux Kernel + GNU Tools + Package Manager + Software


Major families:

### RedHat Family
Examples:

- RHEL
- Rocky Linux
- AlmaLinux
- CentOS Stream

Package manager:


dnf / rpm


Use cases:

Enterprise servers and data centers.

---

### Debian Family

Examples:

- Debian
- Ubuntu
- Linux Mint

Package manager:


apt / dpkg


Used widely in **cloud and DevOps environments**.

---

# Lab Environment

Virtualization platform:


Oracle VirtualBox


VM configuration:

| Resource | Value |
|------|------|
RAM | 4 GB |
CPU | 2 cores |
Disk | 50 GB |

---

# Servers Created

| Server | OS | IP Address |
|------|------|------|
dev-k8s-ubuntulinux-01 | Ubuntu 22.04 | 10.90.121.74 |
dev-k8s-rockylinux-01 | Rocky Linux 9 | 10.90.121.214 |

---

# Hostname Configuration

Ubuntu:


sudo hostnamectl set-hostname dev-k8s-ubuntulinux-01


Rocky:


sudo hostnamectl set-hostname dev-k8s-rockylinux-01


Verify:


hostnamectl


---

# Network Configuration

Initial problem:

Both VMs had same IP:


10.0.2.15


Cause:


VirtualBox NAT networking


Solution:

Changed adapter to:


Bridged Adapter


New IPs:


Ubuntu : 10.90.121.74
Rocky : 10.90.121.214


Command used:


ip a


---

# Time Synchronization

Time synchronization is critical for:

- logging
- authentication
- certificate validation
- distributed systems

Check time:


timedatectl


Enable NTP:


sudo timedatectl set-ntp true


---

# SSH Remote Access

Linux servers are managed using **SSH**.

Provides:

- encrypted remote login
- secure file transfer
- remote command execution

---

## Ubuntu SSH Setup


sudo apt install openssh-server
sudo systemctl start ssh
sudo systemctl enable ssh
systemctl status ssh


---

## Rocky Linux SSH Setup


sudo dnf install openssh-server
sudo systemctl start sshd
sudo systemctl enable sshd
systemctl status sshd


---

# VS Code Remote Development

Remote access configured using **VS Code Remote SSH extension**.

SSH config file:


~/.ssh/config

Host ubuntu-lab
HostName 10.90.121.74
User mani

Host rocky-lab
HostName 10.90.121.214
User mani


Advantages:

- remote file editing
- integrated terminal
- development workflow

---

# Troubleshooting

| Issue | Cause | Solution |
|------|------|------|
Disk not detected | Virtual disk missing | Attach disk |
Same IP | NAT networking | Use bridged adapter |
SSH failure | SSH not installed | Install SSH |
Rocky sleep issue | Power management | Disable suspend |

Command:


sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target


---

# Commands Practiced

### System Information


uname
uname -a
uname -r
uname -n
uname -m
uname -o


### OS Information


cat /etc/os-release
hostnamectl
lsb_release -a


### Networking


ip a
ip link
ip route
ip neigh


### Time


date
timedatectl
uptime


### Storage


lsblk
df -h
du -sh


---

# Day 1 Summary

Successfully built a **Linux server lab environment** with:

- Ubuntu server
- Rocky Linux server
- Network configuration
- Hostname configuration
- Time synchronization
- SSH remote access
- VS Code remote management
