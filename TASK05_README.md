# RabTech Academy - Task 05

## Linux Server Administration & Nginx Reverse Proxy

This repository contains my configuration and notes for Task 05.

## Files

- `nginx.conf` - Nginx reverse proxy configuration
- `LINUX_NGINX_NOTES.md` - Linux, SSH, UFW and Nginx setup notes

## What I worked on

- Linux user and SSH security
- UFW firewall rules for ports 22, 80 and 443
- Nginx reverse proxy
- Gzip compression
- Basic cache headers
- Basic request rate limiting
- HTTPS / SSL configuration notes

## Reverse proxy flow

Client -> Nginx -> Application

Nginx listens for web requests and forwards them to the application running on port 5000.

## Useful checks

```bash
sudo nginx -t
sudo systemctl status nginx
sudo ufw status
ss -tulpn
```

These commands can be used to check the Nginx configuration, service status, firewall status and listening ports.
