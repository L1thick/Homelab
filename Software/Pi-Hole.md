## <u>Port 53 Error</u>
Its that systemd-resolved is what is listening to port 53 & needs to be disabled.
```bash
systemctl disable systemd-resolved.service
systemctl stop systemd-resolved
```

Now you have port 53 released, but there no DNS configured for the host. Edit:
```bash
nano /etc/resolv.conf
```

And add this DNS address for a moment.
```text
nameserver 8.8.8.8
```

Once pihole docker container gets running, you can change the DNS server to the localhost.
```text
nameserver 127.0.0.1
```