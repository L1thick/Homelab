```yml
version: '3'
services:
  sonarr:
    image: lscr.io/linuxserver/sonarr
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /docker/sonarr:/config
      - /media/series:/tv
      - /downloads/complete:/downloads
    ports:
      - 8989:8989
    restart: unless-stopped

  radarr:
    image: lscr.io/linuxserver/radarr
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=America/New_York
    volumes:
      - /docker/radarr:/config
      - /media/movies:/movies
      - /downloads/complete:/downloads
    ports:
      - 7878:7878
    restart: unless-stopped
```