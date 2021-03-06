# ๐ณ docker-8dx: 8dx bots in docker.
ๅไบบ็ใซ้็บใใฆใใ ใใชใชใซใผใ8DX ๅใใฎ Discord Bot ใใณใณใใๅใใใใฎใงใใ

## Services
- [iamtakagi/sokujichan](https://github.com/iamtakagi/sokujichan)
- [iamtakagi/8dx-tracktablebot](https://github.com/iamtakagi/8dx-tracktablebot)
- [iamtakagi/8dx-teambot](https://github.com/iamtakagi/8dx-teambot)

## Installation
`docker-compose.yml`
```yml
version: '3.8'

services:

  db:
    image: mongo
    restart: always
    volumes:
      - db:/data/db
     environment:
       MONGO_INITDB_ROOT_USERNAME: user
       MONGO_INITDB_ROOT_PASSWORD: pass
       MONGO_INITDB_DATABASE: zetsumetsu
       
  sokujichan:
    container_name: sokujichan
    image: iamtakagi/sokujichan:latest
    restart: always
    ports:
      - 8080:8080
    environment:
      # Bot Token (ใใใ ใๆธใๆใใใฐๅใ: ๅฅๅๅฟ้ )
      BOT_TOKEN: xxx
      # Base Uri
      BASE_URI: /
      # Server Host
      HOST: 0.0.0.0
      # Server Port  (ๅฟ่ฆๆฌก็ฌฌใงๆธใๆใใฆใใ ใใ)
      PORT: 8080
      # HOSTNAME (ๅค้จๅฌ้ใใชใๅ ดๅ: null ใงๅฏ)
      HOSTNAME:
      # Logger
      LOG: DEBUG
      # Embed color
      EMBED_COLOR: 83,221,172
      # Mongo DB (ๅบๆฌ็ใซใฏๆธใๆใใชใ)
      MONGO_HOST: db
      MONGO_PORT: 27017
      MONGO_USER: user
      MONGO_PASS: pass

  8dx-tracktablebot:
    container_name: 8dx-tracktablebot
    image: iamtakagi/8dx-tracktablebot:latest
    # Bot Token (ใใใ ใๆธใๆใใใฐๅใ: ๅฅๅๅฟ้ )
    BOT_TOKEN: xxx

  8dx-teambot:
    container_name: 8dx-teambot
    image: iamtakagi/8dx-teambot:latest
    # Bot Token (ใใใ ใๆธใๆใใใฐๅใ: ๅฅๅๅฟ้ )
    BOT_TOKEN: xxx

volumes:
  db:
    driver: local
```

## Start
```console
docker-compose up -d
```
