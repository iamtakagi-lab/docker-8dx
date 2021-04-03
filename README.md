# 🐳 docker-8dx: 8dx bots in docker-compose
個人的に開発している マリオカート8DX 向けの Discord Bot をコンテナに閉じ込めました

# Services
- [iamtakagi/sokujichan](https://github.com/iamtakagi/sokujichan)
- [iamtakagi/8dx-tracktablebot](https://github.com/iamtakagi/8dx-tracktablebot)
- [iamtakagi/8dx-teambot](https://github.com/iamtakagi/8dx-teambot)

## Install
`docker-compose.yml`
```yml
version: '3.8'

services:
  # sokujichan
  sokujichan:
    container_name: sokujichan
    image: iamtakagi/sokujichan:latest
    restart: always
    ports:
      - 8080:8080
    depends_on:
      - mongo
    environment:
      # Bot Token (ここだけ書き換えれば動く: 入力必須)
      BOT_TOKEN: xxx
      # Base Uri
      BASE_URI: /
      # Server Host
      HOST: 0.0.0.0
      # Server Port  (必要次第で書き換えてください)
      PORT: 8080
      # HOSTNAME (外部公開しない場合: null で可)
      HOSTNAME:
      # Logger
      LOG: DEBUG
      # Embed color
      EMBED_COLOR: 83,221,172
      # Mongo DB (基本的には書き換えない)
      MONGO_HOST: mongo
      MONGO_PORT: 27017
      MONGO_USER: user
      MONGO_PASS: pass

  # sokujichan Database  
  sokujichan_mongo:
    image: mongo
    container_name: sokujichan_mongo
    restart: always
    volumes:
      - ./mongodb:/data/db
    environment:
      MONGO_INITDB_ROOT_USERNAME: user
      MONGO_INITDB_ROOT_PASSWORD: pass
    ports:
      - 27017:27017

  # TracktableBot
  8dx-tracktablebot:
    container_name: 8dx-tracktablebot
    image: iamtakagi/8dx-tracktablebot:latest
    # Bot Token (ここだけ書き換えれば動く: 入力必須)
    BOT_TOKEN: xxx

  # TeamBot
  8dx-teambot:
    container_name: 8dx-teambot
    image: iamtakagi/8dx-teambot:latest
    # Bot Token (ここだけ書き換えれば動く: 入力必須)
    BOT_TOKEN: xxx
```

## Start
```console
docker-compose up -d
```
