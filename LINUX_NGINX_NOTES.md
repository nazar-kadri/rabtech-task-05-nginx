# RabTech Academy - Task 05

## Linux Server Administration & Nginx Reverse Proxy

This is the configuration plan I prepared for the task.

## 1. Linux user and SSH

- Create a normal user for daily work.
- Give the user sudo access only when needed.
- Use SSH keys for server login.
- Disable password-based SSH after key login is tested.

Example SSH setting:

```text
PasswordAuthentication no
```

Keep one tested SSH session open before restarting SSH after making this change.

## 2. UFW firewall

Only the required ports should be open:

```bash
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw enable
sudo ufw status
```

Port 22 is for SSH, 80 is for HTTP and 443 is for HTTPS.

## 3. Nginx reverse proxy

Nginx accepts the request first and forwards it to the application running on port 5000.

```text
Client
  |
  v
Nginx :80 / :443
  |
  v
Application :5000
```

The `nginx.conf` file in this repository contains the reverse-proxy, gzip, caching and rate-limit settings.

## 4. Gzip compression

Gzip reduces the size of suitable text responses before sending them to the client.

This can help reduce bandwidth usage and improve page loading for larger text-based responses.

## 5. Cache headers

Static files such as CSS and JavaScript can be cached for a period of time.

The configuration uses:

```text
Cache-Control: public, max-age=604800
```

This means the browser can reuse the cached static file for 7 days.

## 6. Rate limiting

The configuration uses a basic request rate limit.

```text
rate=5r/s
burst=10
```

This is a simple protection against a client sending too many requests in a short time.

## 7. SSL / HTTPS

For a real public server, HTTPS can be configured with a certificate such as Let's Encrypt.

For a sandbox or lab, a self-signed certificate can be used for testing.

Example Nginx SSL directives:

```nginx
listen 443 ssl;
ssl_certificate /path/to/fullchain.pem;
ssl_certificate_key /path/to/privkey.pem;
```

A real certificate and domain are required for a normal public HTTPS setup.

## 8. Checks after configuration

Useful checks:

```bash
sudo nginx -t
sudo systemctl status nginx
sudo ufw status
ss -tulpn
```

`nginx -t` checks the Nginx configuration syntax before reloading the service.

## Notes

The commands above are a configuration and testing guide for the internship task. Actual server changes should be done on the lab/server environment assigned for the task.
