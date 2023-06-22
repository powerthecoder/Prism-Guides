# Basic CyberSecurity Guide (Linux)

## Connecting to the Server

If you have never connected to your server's Command Line Interface (CLI), this guide will teach you how to connect to the server via SSH (Secure Shell Protocol).

There are a few ways to SSH into a server. You can either use your computer's terminal/command prompt or install an SSH client such as PuTTY or Termius.


**Links to SSH Clients:**

![PuTTY](</Pictures/Basic_Sec_Guide/Basic_Sec_Guide1.png>)
- [PuTTY](https://www.chiark.greenend.org.uk/~sgtatham/putty/latest.html)

![Termius](</Pictures/Basic_Sec_Guide/Basic_Sec_Guide2.png>)
- [Termius](https://account.termius.com/)

In this example, we will use the IP Address 192.168.1.2, the default SSH port is 22, the username is "root," and the password is "myguide".

**How to SSH with PuTTY:**
1. Download and install PuTTY from the provided link.
2. Launch PuTTY.
3. Enter the server's IP address and port number.
4. Select the SSH connection type.
5. Click "Open" to establish the SSH connection.

![SSH with PuTTY](</Pictures/Basic_Sec_Guide/Basic_Sec_Guide3.png>)

**How to SSH with Termius:**
1. Install Termius from the provided link.
2. Launch Termius.
3. Create a new host and enter the server's IP address, port number, username, and password.
4. Save the host configuration.
5. Connect to the server by selecting the saved host.

![SSH with Termius](</Pictures/Basic_Sec_Guide/Basic_Sec_Guide4.png>)

## What Does the Script Do?

Once you successfully log into your Linux server, you can either manually install and configure security settings and software, or you can run a custom GitHub script that automates most security configurations and software installations.

The script will automatically perform the following tasks:

- Update and upgrade the system.
- Install and configure unattended-upgrades.
- Install and configure fail2ban.
- Install and configure UFW (Universal Firewall).
- Configure UFW to protect against port scans and bot attacks.
- Install and configure sshd (SSH server).
- Configure IPTables for port scanning and bot attacks.
- Install and configure portsentry.
- Install and configure sshguard.
- Install and run chrootkit.
- Create a new user for sudo access and disable root login.

Please make sure to run this script with sudo or root privileges for it to run properly.

**Notice:** At the end of the script, it will ask you to create a new user. Follow the steps in the script carefully, as it will disable the root user and no longer allow SSH login with the root user.
[Link to Script](https://github.com/powerthecoder/Linux-CybSec)

## What Are Ports and How to Open/Close Them?

Ports can be thought of as doors to your server. Opening a port allows communication channels for software to send and receive data through the firewall. It's like poking a hole in the firewall to allow specific types of traffic.

Here is a list of common ports that applications use:

![Port List](</Pictures/Basic_Sec_Guide/Basic_Sec_Guide5.png>)

To configure ports on your server, you can use UFW (Universal Firewall). UFW is a firewall configuration tool for Linux machines that provides an easy way to set up a basic but efficient firewall.

First, make sure to download UFW by running the following command:

``` shell
root@guide:~# sudo apt-get install ufw
```

Once UFW is downloaded, you can start configuring it for your needs. First, identify the services that require specific open ports. To open port 22 for SSH, use the following command:

``` shell
root@guide:~# sudo ufw allow 22
```

For example, to open port 3306 as TCP and block port 53 as UDP, you can use the following commands:

``` shell
root@guide:~# sudo ufw allow 3306/tcp
Rules updated
Rules updated (v6)
root@guide:~# sudo ufw deny 53/udp
Rules updated
Rules updated (v6)
root@guide:~# 
```

Please ensure that you carefully consider the implications of

Once you are done with opening/closing ports and configuring your UFW you can go ahead and enable it now by doing the following command

``` shell
root@guide:~# systemctl start ufw
root@guide:~# ufw enable
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
root@guide:~# 
```

