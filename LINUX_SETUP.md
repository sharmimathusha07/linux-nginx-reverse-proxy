# Linux Server Administration and Security

## 1. Project Overview

This project documents Linux server security configuration, SSH access control, UFW firewall rules, and Nginx reverse proxy setup.

## 2. Linux User and Permissions

Create a dedicated administrative user:

```bash
sudo adduser adminuser
sudo usermod -aG sudo adminuser
```

Set appropriate permissions for SSH files and directories. Avoid giving unnecessary users administrator privileges.

## 3. SSH Key Authentication

Generate an SSH key on the client computer:

```bash
ssh-keygen -t ed25519
```

Copy the public key to the server:

```bash
ssh-copy-id adminuser@YOUR_SERVER_IP
```

Test key-based login in a new terminal before disabling password authentication.

Edit the SSH server configuration:

```bash
sudo nano /etc/ssh/sshd_config
```

Set or verify these options:

```text
PubkeyAuthentication yes
PasswordAuthentication no
PermitRootLogin no
```

Validate and reload SSH:

```bash
sudo sshd -t
sudo systemctl reload ssh
```

On some distributions, the service may be named `sshd`. Keep an existing session open and confirm key-based login works before closing it.

## 4. UFW Firewall Configuration

Install UFW if necessary, then configure the allowed ports:

```bash
sudo apt update
sudo apt install ufw -y

sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp

sudo ufw enable
sudo ufw status numbered
```

Only SSH, HTTP, and HTTPS are explicitly allowed by these rules. Confirm SSH access and any cloud-provider firewall settings before enabling UFW to avoid losing access.

## 5. Install and Configure Nginx

```bash
sudo apt install nginx -y
sudo systemctl enable --now nginx
sudo nginx -t
```

Copy the project's `nginx.conf` into the appropriate Nginx configuration location and adapt it to the server's existing configuration. Do not overwrite the system configuration without checking it first.

The example configuration includes:
- HTTP-to-HTTPS redirection
- Reverse proxying to an application on port 3000
- Gzip compression
- Rate limiting
- Security headers and caching headers

## 6. Verification

Check firewall rules:

```bash
sudo ufw status verbose
```

Check Nginx syntax and service status:

```bash
sudo nginx -t
sudo systemctl status nginx
```

Test SSH key authentication from a separate terminal before ending the current session.

## 7. Security Notes

- Use SSH keys and protect the private key.
- Keep the operating system and packages updated.
- Allow only required network ports.
- Use a valid TLS certificate for production.
- Review logs and monitor failed login attempts.
- Test configuration changes before reloading services.

## 8. Implementation Status

This repository contains configuration examples and setup documentation. Actual server security depends on running and verifying these steps on a Linux server.
