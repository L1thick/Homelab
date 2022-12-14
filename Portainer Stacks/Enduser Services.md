```yml
version: '3'
services:
  plex:
    image: lscr.io/linuxserver/plex
    container_name: plex
    network_mode: host
    environment:
      - PUID=1000
      - PGID=1000
      - VERSION=docker
    volumes:
      - /docker/plex/config:/config
      - /tmp/plexTranscodes:/transcode
      - /media/series:/tv
      - /media/movies:/movies
    restart: unless-stopped

  ombi:
    image: lscr.io/linuxserver/ombi
    container_name: ombi
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /docker/ombi:/config
    ports:
      - 3579:3579
    restart: unless-stopped
```