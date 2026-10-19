# SSL/TLS Configuration Guide

## 1. Overview

SSL/TLS encrypts traffic between clients and the Nginx web server. This guide explains how to use a self-signed certificate in a sandbox and Let's Encrypt for a public production server.

## 2. Option A: Self-Signed Certificate for Sandbox Testing

Create a self-signed certificate on the Linux server:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
  -keyout /etc/ssl/private/nginx-selfsigned.key \
  -out /etc/ssl/certs/nginx-selfsigned.crt \
  -subj "/CN=localhost"
```

Set restrictive permissions on the private key:

```bash
sudo chmod 600 /etc/ssl/private/nginx-selfsigned.key
```

The certificate paths match the example paths in `nginx.conf`.

A self-signed certificate is suitable for a sandbox, but browsers will normally show a security warning because it is not signed by a publicly trusted certificate authority.

## 3. Option B: Let's Encrypt for a Public Server

Requirements:
- A domain name pointing to the server's public IP address.
- Inbound ports 80 and 443 allowed.
- Nginx installed and running.

Install Certbot on Ubuntu:

```bash
sudo apt update
sudo apt install certbot python3-certbot-nginx -y
```

Request a certificate for your real domain:

```bash
sudo certbot --nginx -d your-domain.example
```

Replace `your-domain.example` with your own domain name. Do not use this placeholder literally.

Certbot can configure Nginx to use the issued certificate. Verify the configuration afterwards:

```bash
sudo nginx -t
sudo systemctl reload nginx
```

## 4. Certificate Renewal

Check the renewal process:

```bash
sudo certbot renew --dry-run
```

## 5. Verification

For a configured HTTPS server, test the response:

```bash
curl -I https://your-domain.example
```

For local sandbox testing, use the hostname and certificate that you configured. A self-signed certificate may require special handling by the test client.

## 6. Security Notes

- Never publish or commit private keys to GitHub.
- Use a trusted certificate for public production websites.
- Keep certificates renewed and monitor expiry dates.
- TLS configuration must be tested on the actual server.

## 7. Implementation Status

This file documents the SSL/TLS setup procedure. Creating this document alone does not issue a certificate or enable HTTPS on a server.
