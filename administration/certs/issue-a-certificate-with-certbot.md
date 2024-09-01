# Issue a certificate with certbot

### Install

```bash
sudo apt install certbot
```

### Checking SSL configuration

```bash
sudo certbot certificates
```

### Launching a temporary web server to verify domain ownership

```bash
sudo certbot certonly --standalone -d example.com -d www.example.com
```

### Using Manual mode

Режим `manual` подходит, если вы не можете временно остановить ваш веб-сервер или если хотите выполнить проверку вручную, например, если ваш сервер не имеет прямого доступа к интернету.

```bash
sudo certbot certonly --manual -d example.com -d www.example.com
```

### Verify domain ownership with DNS TXT record

```bash
sudo certbot certonly --agree-tos --manual --preferred-challenges dns -d "*.$DOMAIN" --register-unsafely-without-email
```
