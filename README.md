# SSH-Hardening

## Introduction

Hardening the SSH aspect of a Linux server and explaining each action and why it is needed. the final goal is to automate the entire process with a bash script that will save time and avoid human errors.

The operating system used in this project is Ubuntu 24.04.2 that resides on a VM with the next resources:
- RAM: 2048 MB
- CPU: 2
- Storage: 10 GB

The resources allocation process is based on the official recommendation in the installation guide by Ubuntu.

# Step 1 - Upgrading OpenSSH to the latest version

Most of the servers will already have the SSH installed, the typical installation is using a package manager specific for the distribution of the Linux, in my case its apt that is used on Ubuntu.

The apt is a binary that fetches packages from the CDN (Content Delivery Network) that contains different packages that were checked by the developers and added as the official tested package, and most of the times the version of those packages are not the latest and this weakens the server.

While doing this project the official tested version of OpensSSH for Ubuntu 24.04.2 was 9.9p1 which is not the latest, if you visit the [Release Notes](https://www.openssh.com/releasenotes.html) of the OpenSSH you will see that the following version which is 9.9p2 has security fixes like CVE-2025-26466 which allows DOS attacks.

Here are the basic steps to achieve that:

`username@hostname~$ ssh -V`<br/>
`OpenSSH_9.6p1 Ubuntu-3ubuntu13.12`

First check if SSH is installed and its version, if not installed jump to the installation section, if installed then follow the next step

**BEFORE THE NEXT STEP, DON'T DO IT WHILE REMOTELY CONNECTED WITH SSH OTHERWISE YOU WILL BRICK YOURSELF FROM THE SYSTEM AND WILL HAVE TO DO IT LOCALY**

`sudo apt list --installed | grep ssh`

You will see 5 rows when each is a package related to ssh that you will have to delete

`sudo apt remove openssh-client`

This will remove all the packages related to ssh

Now installing the latest OpenSSH version from the official source, you can go to [https://www.openssh.com/releasenotes.html](https://www.openssh.com/releasenotes.html) and copy the download link for the OpenSSH binaries.
