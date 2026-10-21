# Born2beroot

> **A 42 School system-administration project focused on virtualization, Linux security, and server hardening.**

## Project Overview

**Born2beroot** is a practical infrastructure project from the [42 School](https://42.fr) curriculum. Its objective is to design, install, configure, and secure a Linux virtual machine while applying strict security and administration practices.

The project provides hands-on experience with the day-to-day responsibilities of a system administrator: managing users and permissions, securing remote access, configuring a firewall, controlling services, and monitoring system resources.

Rather than focusing on application development, Born2beroot emphasizes the secure and disciplined management of the operating system beneath modern software systems.

## Objectives

- Deploy a functional Linux server inside a virtual machine.
- Apply strict security and access-control policies.
- Manage users, groups, passwords, and administrative privileges.
- Configure secure remote administration using SSH.
- Install and configure a firewall with minimal network exposure.
- Manage system services and ensure that only required services are enabled.
- Monitor system performance and resource usage.
- Automate recurring checks with shell scripting.
- Document configuration choices so the environment remains reproducible and maintainable.

## Main Areas Covered

### Operating System Administration

- Linux installation and partitioning
- Package management and system updates
- Hostname and network configuration
- Service supervision with `systemd`
- Secure handling of system files and directories

### Identity and Access Management

- User and group creation
- Password-policy enforcement
- Sudo configuration and privilege limitation
- File ownership and permission management
- Access control based on the principle of least privilege

### Network Security

- SSH configuration for secure remote administration
- Firewall configuration using `UFW` or `iptables`
- Restriction of exposed ports and network services
- Validation of listening services and active connections

### Monitoring and Automation

- System resource monitoring
- Reporting of CPU, memory, disk, and processor information
- Shell scripting for automated status checks
- Scheduled execution with `cron` or `crontab`

## Technologies and Tools

- **Operating system:** Debian or another distribution required by the project subject
- **Virtualization:** VirtualBox
- **Shell:** Bash
- **Remote administration:** OpenSSH
- **Firewall:** UFW / iptables
- **Service management:** systemd / systemctl
- **Automation:** cron / crontab
- **Version control:** Git

## Installation and Setup

1. Create a new virtual machine in VirtualBox.
2. Install the selected Linux distribution using the project requirements.
3. Configure disk partitions, users, groups, and authentication policies.
4. Install and configure SSH, the firewall, and the required system services.
5. Apply the security-hardening rules defined by the project subject.
6. Configure the monitoring script and schedule its execution.
7. Verify the server configuration, permissions, services, and network exposure.

> The exact commands and configuration values should be adapted to the official Born2beroot subject and the chosen operating system.

## Repository Contents

This repository contains the documentation and configuration references used to build, secure, and validate the Born2beroot virtual machine. Typical materials include:

- Configuration notes and installation procedures
- Bash scripts for system monitoring and administration
- SSH, firewall, sudo, and password-policy references
- Validation checklists for project evaluation
- Explanations of security decisions and administrative commands

## Learning Outcomes

By completing this project, I developed practical knowledge of:

- Linux system architecture and server administration
- Virtual machine deployment and maintenance
- User, group, and permission management
- Secure remote access and firewall configuration
- Service management and system monitoring
- Shell scripting and task automation
- Security hardening and least-privilege principles
- Technical documentation and reproducible configuration

## Project Status

**Completed and validated as part of the 42 curriculum.**

## Author

**A-chem**  
42 School student
