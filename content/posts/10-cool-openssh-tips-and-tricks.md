---
title: 10 Cool OpenSSH tips and tricks
description: 
date: 2024-10-04
tags:
  - linux
  - openSSH
toc: true
---
### Introduction:
OpenSSH is a free, open-source tool used to securely connect to remote systems, transfer files, and create secure tunnels. In this post, we'll explore 10 tips and tricks to help you use OpenSSH more effectively and securely.

---

### 1. **Basic SSH Connection**

```bash
ssh user@remote_host
```
If your server runs SSH on another port (e.g., 2222), you can connect using:

```bash
ssh -p 2222 user@remote_host
```

---

### 2. **Password-less SSH Login using SSH Keys**

**Step 1: Generate an SSH key pair** on your local machine:
  ```bash
  ssh-keygen -t ed25519 -C "your_email@example.com"
  ```
**Step 2: Copy the public key to the remote server**:
  ```bash
  ssh-copy-id user@remote_host
  ```
  This command installs your public key on the remote server, allowing you to log in without a password.

---

### 3. **Using the SSH Config File for Simplified Connections**

For example:
```bash
Host server1
  HostName server1.example.com
  User user
  Port 2222
  IdentityFile ~/.ssh/id_rsa
```

With this setup, you can connect to `server1` simply by typing:
```bash
ssh server1
```

---

### 4. **Remote Command Execution via SSH**
You can execute commands remotely using SSH. For instance:

```bash
ssh user@remote_host "df -h"
```

**Bonus**: Combine SSH with a loop to run commands on multiple servers:
```bash
for server in server1 server2 server3; do
  ssh $server "uptime"
done
```

---

### 5. **SSH Tunneling for Port Forwarding**
Forward ports from your local machine to a remote server. It's useful for people who can't open ports on their routers or have certain ports blocked by their ISP.

**Local Port Forwarding**: Forward a port on your local machine to a port on a remote server:
  ```bash
  ssh -L local_port:remote_host:remote_port user@remote_host
  ```

  Example: Forward your local port 8080 to access a web service on the remote host’s port 80:
  ```bash
  ssh -L 8080:localhost:80 user@remote_host
  ```

**Reverse Port Forwarding**: Forward a remote port to your local machine:
  ```bash
  ssh -R remote_port:localhost:local_port user@remote_host
  ```

  Example: Make a service on your local machine available to a remote server:
  ```bash
  ssh -R 8080:localhost:80 user@remote_host
  ```

---

### 6. **SSH Proxying with ProxyJump**
Connect to a remote server through an intermediate (jump) host using a single SSH command. 

You may wonder how this feature is useful. Imagine you have a database server on a private network that isn’t directly accessible from the internet due to security restrictions. To reach this database server, you must first log in to a jump server, which is the only server exposed to the internet.

For example:
```bash
ssh -J jump_host user@target_host
```

You can also configure this in your SSH config file:
```bash
Host target_host
  HostName target_host.example.com
  User user
  ProxyJump jump_host.example.com
```

---

### 7. **Using SCP for Secure File Transfers**
You can transfer files between your local machine and a remote server using SCP. 
For example, to copy a file from your local machine to the remote server:

```bash
scp file.txt user@remote_host:/path/to/destination/
```

Similarly, you can retrieve a file from a remote server to your local machine:

```bash
scp user@remote_host:/path/to/file.txt /local/destination/
```

---

### 8. **SSHFS: Mount Remote Directories Locally**
Mount a remote server's directory as if it were a local directory. First, ensure SSHFS is installed on your local machine, then run:

```bash
sshfs user@remote_host:/remote/directory /local/mount/point
```

---

### 9. **Enable Two-Factor Authentication (2FA)**
OpenSSH supports two-factor authentication (2FA). You can configure 2FA using Google Authenticator or other OTP solutions.

 **Step 1**: Install the necessary packages on your server:
  ```bash
  sudo apt-get install libpam-google-authenticator
  ```

 **Step 2**: Run `google-authenticator` on your server and follow the prompts to set it up.

 **Step 3**: Configure SSH to require both a password and an OTP by editing `/etc/ssh/sshd_config`:
  ```bash
  ChallengeResponseAuthentication yes
  ```

---

### 10. **Monitoring and Logging SSH Sessions**
To keep track of who is accessing your servers, you can enable logging of all SSH sessions. Use `last` to view previous login attempts:

```bash
last -a
```

---

### Conclusion:
OpenSSH is an amazing tool that I absolutely love! Its versatility, from password-less authentication to advanced tunneling techniques, makes remote operations simple and secure. By mastering its features, you can significantly enhance efficiency and streamline your workflow.

OpenSSH is a work of art!
