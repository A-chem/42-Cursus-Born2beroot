
**UFW** stands for **Uncomplicated Firewall**, and it is a front-end tool for managing the **iptables** firewall in Linux. UFW provides an easier way to configure a firewall and manage network access on a system.

A **firewall** is a network security system that monitors and controls incoming and outgoing network traffic based on predetermined security rules. It acts as a barrier between a trusted internal network and untrusted external networks, like the internet.

In Linux, [[iptables]] is the actual firewall tool, but it can be complex to manage directly. **UFW** makes it easier to configure and use.

## UFW Basics

UFW allows you to configure rules to either allow or deny traffic on specific ports or to/from specific IP addresses.

## UFW Commands Overview

1. **Check UFW Status**: `sudo ufw status`
2. **Enable UFW**: `sudo ufw enable`
3. **Disable UFW**: `sudo ufw disable`
4. **Allow Traffic on a Specific Port**: `sudo ufw allow 22` you can specify the port with a protocol: `sudo ufw allow 22/tcp`

5. **Allow Traffic for a Specific Service**:  `sudo ufw allow ssh`
6. **Deny Traffic on a Specific Port**: `sudo ufw deny 80`
7. **Delete a Rule**: `sudo ufw status numbered`
8. **Allow or Deny a Specific IP**: `sudo ufw allow from 192.168.1. , sudo ufw deny from 192.168.1.100 
9. **Allow Traffic on a Range of Ports**: `sudo ufw allow 8000:8080/tcp`
10. **Check UFW Logs**: `sudo less /var/log/ufw.log`








### Example:

- If you want to allow SSH access (for remote login), you would run
    
    `sudo ufw allow 22`
    
    This allows people to connect to your system using SSH.