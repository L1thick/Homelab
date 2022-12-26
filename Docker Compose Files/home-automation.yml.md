```yml
version: "3"
services:
  deconz:
    image: deconzcommunity/deconz:stable
    container_name: deconz
    restart: always
    privileged: true
    ports:
      - 80:80
      - 443:443
    volumes:
      - /docker/deCONZ:/opt/deCONZ
    devices:
      - /dev/ttyACM0                 # USB device with Conbee II
    environment:
      - TZ=America/New_York
      - DECONZ_WEB_PORT=80
      - DECONZ_WS_PORT=443
      - DEBUG_INFO=1
      - DEBUG_APS=0
      - DEBUG_ZCL=0
      - DEBUG_ZDP=0
      - DEBUG_OTA=0
      - DEBUG_HTTP=0
      - DECONZ_DEVICE=/dev/ttyACM0   # USB device with Conbee II
      - DECONZ_START_VERBOSE=0
      - 
    homeassistant:
    image: lscr.io/linuxserver/homeassistant:latest
    container_name: homeassistant
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /docker/homeassistant:/config
    ports:
      - 8123:8123
    restart: unless-stopped
```