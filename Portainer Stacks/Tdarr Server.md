```yml
version: '3'
services:
  tdarr:
    container_name: tdarr
    image: ghcr.io/haveagitgat/tdarr:latest
    restart: unless-stopped
    network_mode: bridge
    ports:
      - 8265:8265 # webUI
      - 8266:8266 # Server
      - 8267:8267 # Internal
    environment:
      - TZ=America/New_York
      - PUID=1000
      - PGID=1000
      - UMASK_SET=002
      - serverIP=192.168.1.10
      - serverPort=8266
      - webUIPort=8265
      - internalNode=true
      - nodeID=Veronica

    volumes:
      - /docker/tdarr/server:/app/server      
      - /docker/tdarr/configs:/app/configs      
      - /docker/tdarr/logs:/app/logs
      - /docker/tdarr/temp:/temp
```