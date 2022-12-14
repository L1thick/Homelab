```yml
version: '3'
services:

  sabnzbd:
    container_name: sab
    image: linuxserver/sabnzbd
    network_mode: service:gluetun
    volumes:
      - /docker/sabnzbd:/config
      - /downloads/complete:/downloads
      - /downloads/incomplete/downloading:/incomplete-downloads
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=American/New_York
    restart: unless-stopped
    
  transmission:
    image: lscr.io/linuxserver/transmission
    container_name: trans
    network_mode: service:gluetun
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America\New_York
      - TRANSMISSION_WEB_HOME=/combustion-release/
    volumes:
      - /docker/trans:/config
      - /downloads/incomplete/av_processing:/downloads/complete
      - /downloads/incomplete/downloading:/downloads/incomplete
    restart: unless-stopped

  gluetun:
    image: qmcgaw/gluetun
    container_name: gluetun
    cap_add:
      - NET_ADMIN
    devices:
      - /dev/net/tun:/dev/net/tun
    ports:
      - 8888:8888/tcp # HTTP proxy
      - 7092:8080 # SabNZBD
      - 7091:9091 #Transmission
      - 51413:51413 #Transmission
      - 51413:51413/udp #Transmission
    volumes:
      - /docker/gluetun:/gluetun
    environment:
      - VPN_SERVICE_PROVIDER=protonvpn
      - OPENVPN_USER=
      - OPENVPN_PASSWORD=
      - SERVER_COUNTRIES=Switzerland
    restart: unless-stopped

  docker-av:
    image: rordi/docker-antivirus
    container_name: docker-av
  # command:
  #   - /usr/local/install_alerts.sh @icloud.com
    volumes:
      - /downloads/incomplete/av_processing:/data/av/queue
      - /downloads/complete:/data/av/ok
      - /downloads/quarantine:/data/av/nok
      - /downloads/quarantine:/data/av/quarantine
      - /downloads/incomplete/av_processing:/data/av/scan
```