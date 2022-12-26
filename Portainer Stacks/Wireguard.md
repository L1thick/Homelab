```yml
version: "2.1"

services:
  wireguard:
    image: linuxserver/wireguard
    container_name: wireguard
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=American/New_York
      - SERVERURL=auto
      - SERVERPORT=00000
      - PEERS=3
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.13.13.0
    volumes:
      - /docker/wireguard/config:/config
      - /lib/modules:/lib/modules
    ports:
      - 00000:00000/udp
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
    restart: unless-stopped
```