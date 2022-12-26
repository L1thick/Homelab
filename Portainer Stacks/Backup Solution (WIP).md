```yml
version: "3"
services:
  duplicati:
    image: lscr.io/linuxserver/duplicati:latest
    container_name: duplicati
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=American/New_York
      - CLI_ARGS= #optional
    volumes:
      - /docker/duplicati:/config
      - /backups:/backups
      - /docker:/source
    ports:
      - 8200:8200
    restart: unless-stopped
```