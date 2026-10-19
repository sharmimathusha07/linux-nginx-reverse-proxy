# Linux Server Administration & Nginx Reverse Proxy

## Project Overview

This project demonstrates Linux server security concepts and an Nginx reverse proxy configuration with HTTPS, gzip compression, caching headers, and rate limiting.

## Objectives

- Document Linux user administration and permissions.
- Configure SSH key-based authentication.
- Restrict network access using UFW firewall rules.
- Configure Nginx as a reverse proxy.
- Document SSL/TLS setup using self-signed certificates or Let's Encrypt.

## Repository Structure

```text
linux-nginx-reverse-proxy/
├── nginx.conf
├── LINUX_SETUP.md
├── SSL_SETUP.md
└── README.md
```

## Technologies Used

- Linux / Ubuntu
- OpenSSH
- UFW Firewall
- Nginx
- OpenSSL
- Let's Encrypt Certbot

## Configuration Features

- HTTP to HTTPS redirection
- TLS configuration
- Reverse proxy to an application on port 3000
- Gzip compression
- Request rate limiting
- Security and caching headers
- SSH and firewall setup documentation

## Implementation

Refer to `LINUX_SETUP.md` for Linux and firewall setup instructions.

Refer to `SSL_SETUP.md` for sandbox and production SSL/TLS setup.

Review `nginx.conf` for the sample Nginx configuration.

## Important Security Notes

The configuration files are examples and documentation. A real Linux server must be configured and tested before these features can be considered active. Self-signed certificates are for sandbox testing; production deployments should use a trusted certificate.

Private keys, passwords, tokens, and other secrets must never be committed to this repository.

## Verification Checklist

- [ ] SSH key login tested
- [ ] Password-based SSH login disabled safely
- [ ] UFW rules verified
- [ ] Nginx configuration test passed
- [ ] HTTPS certificate configured
- [ ] Reverse proxy tested
- [ ] Rate limiting and response headers verified

## Author

Sharmi Mathusha M S 
