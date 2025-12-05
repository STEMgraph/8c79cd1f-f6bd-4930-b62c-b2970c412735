<!---
{
  "id": "8c79cd1f-f6bd-4930-b62c-b2970c412735",
  "teaches": "Introduction to Secure Shell Protocol",
  "depends_on": ["bccc53a1-ca6e-4995-8ce9-10958bf9e1f9", "2c7334b3-b07d-48d6-a562-79072d8e166e"],
  "author": "Stephan Bökelmann",
  "first_used": "2025-03-21",
  "keywords": ["network", "user", "SSH", "administration"]
}
--->

# Introduction to Secure Shell Protocol

## 1) Introduction

When you connect a terminal directly to a computer—be it through a keyboard and screen or an old-school teletype printer—the input and output are handled by the local operating system. In such a local setup, communication between you and the machine happens through a *shell*, a program that interprets commands and launches other programs accordingly.

But what happens when you want to connect to a computer *remotely*? Meaning, a computer that is not located right in front of you, but reachable via a TCP/IP network-connection. Maybe the device is located in a different room, a data center, or another country. That’s where the **Secure Shell Protocol**, or **SSH**, becomes essential.

SSH is a cryptographic network protocol that allows secure communication over an insecure network. It lets you log in to remote computers, execute commands, transfer files, or even tunnel other network connections—all in a secure, encrypted way.

SSH was born out of the need for security in the early days of the internet. In the 1990s, the Telnet protocol was widely used, but it transmitted passwords and data in plaintext, making it easy to intercept. In 1995, Finnish researcher Tatu Ylönen created SSH to address this vulnerability. Today, SSH is one of the most essential tools for system administrators, developers, DevOps engineers, and many others working with networked devices.

To use SSH, two components are needed:
1. A **server** (running the SSH daemon `sshd`) that listens for incoming connections.
2. A **client** that initiates the connection to the server.

Modern Linux systems usually have the SSH client preinstalled. The server component may need to be installed and configured. On Windows and macOS, an SSH client is typically available by default as well.

In this exercise, you will:
- Set up a Linux system (a Raspberry Pi or a virtual server),
- Install and configure the OpenSSH server,
- Create a new user account,
- Connect to the machine over the network using SSH,
- Understand how host authentication and user login work.

Through this, you’ll gain practical experience in:
- Linux system administration,
- Basic networking,
- Remote access and security principles.

You’ll also begin to see why SSH is not just a tool for “admins,” but a fundamental skill for anyone working in computer science, engineering, or IT. It allows secure access to headless devices (like embedded systems), remote development environments, and distributed systems.


### 1.1) Further Readings and Other Sources
History of SSH – Interview mit Tatu Ylönen
- [SSH on Computerphile](https://www.youtube.com/watch?v=ORcvSkgdA58)
- [SSH Crashcourse](https://www.youtube.com/watch?v=hQWRp-FdTpc)
- [Q&A with Tatu Ylönen](https://www.youtube.com/watch?v=MbnMRi7664s)

## 2) Tasks
1. **Order a Machine**: Set up a Raspberry Pi according to the standard procedure with Raspbian installed or get a Linux-Server from a Cloud-Provider. If none of this is possible for you, use the [STEMgraph-forum](https://github.com/orgs/STEMgraph/discussions) to ask the community for a machine. This will be our *Remote-Host*.
2. **Install Open SSH**: When you have console access to the machine, install the _Open-SSH_-Server via `sudo apt install openssh-server`.
3. **Inspect**: Use the `less`-pager to inspect the `/etc/ssh/sshd_conf` file. Read it line for line and take notes if you find anything that already looks familiar to you.
4. **Enable PW Login**: Usually we would not enable *PW* authentication over SSH, but for practical reasons we will activate it for now. Find the line `PasswordAuthentication` and set it to `yes`.
5. **Setting up a user**: Set up a new user with `adduser`. Choose a secure PW.
6. **Initial Login**: Use `su` to verify everything worked as intended.
7. **Networking**: Make sure, that your machine is connected to a network, and that it received an IP-address. Inspect it with `ip addr show`. If you are not familiar with this command check out the previous [networking-exercise](www.github.com/STEMgraph).
8. **Ping**: Note the IP address of your device and move to your usual terminal-device. Launch a new shell session and use the `ping` command to make sure, that the device is reachable from your terminal. If not, you might not be connected to the same network!
9. **Remote Login**: On older machines, you might have to install an _SSH-Client_-Software. No matter, whether you are using Windows, Linux, or MacOS: the SSH client should already be installed. We now want to login to the remote-host with the newly created user: `ssh <new_user>@<remote-host-ip>`. If everything is setup correctly, you will be asked, whether you want to store the _fingerprint_ of the remote-host in your _known-hosts_-file. Accept this by typing `yes`. Wait for the password-prompt and punch in the newly created users password. You are now logged in via _SSH_.
10. **Exit**: Type `exit` and press the enter key. You are now back on your local machine.
11. **Wrong User**: Type `ssh <remote-host-ip>`. Do not use the `<new_user>@` in front of it. Take notes what happens.

## 3) Questions
1. What reason do we need _SSH_ for?
2. What is necessary to be able to log in via _SSH_?
3. Why are we asked to store the _fingerprint_ of the remote-host?
4. Why does the login-attempt from task 11 not work?


## 4) Advice
Although we started with **password authentication**, this method is not recommended in professional environments due to its vulnerability. In future exercises, we will switch to **public key authentication**, a much more secure and flexible approach.
