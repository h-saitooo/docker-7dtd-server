# Docker 7 Days to Die Server

Base image: https://hub.docker.com/r/vinanrra/7dtd-server

ベースイメージはLinux GSMも同梱されているため、Linux GSMが提供する機能も利用可能

Linux GSM: https://docs.linuxgsm.com/

## 使い方

### 1. ゲームのインストール

```bash
git clone https://github.com/h-saitooo/docker-7dtd-server.git
cd docker-7dtd-server
docker compose up -d

# 進捗確認
docker compose logs

# コンテナの状況確認
docker compose ps

# 実行中コンテナのステータスがRestartingになったら初期化終了
# 一旦コンテナを停止させる
docker compose down -v
```

### 2. ゲーム設定ファイルの変更
サーバー名やサーバーパスワード、ゲーム自体の設定などの変更を行う

#### 変えたほうがいいところ
- サーバーパスワード
- Telnetパスワード

```
vim volumes/ServerFiles/sdtdserver.xml
```

参考

[serverconfig.xml](https://7daystodie.fandom.com/wiki/Server:_serverconfig.xml)
[7DTDサーバ特有のセキュリティ対策](https://higashi-kyoto.tokyo/?page_id=573)

### 3. サーバーの起動

1. `compose.yml` の `START_MODE` を `1` に変更する
1. `docker compose up -d`

### 4. サーバーの停止

```
docker compose down -v
```

## ゲームサーバーのアップデート

```
1. `compose.yml` の `START_MODE` を `3` に変更する
1. `docker compose up -d`
```

## Discordにサーバー通知を送る設定

```bash
vim ./volumes/LGSM-Config/common.cfg

discordalert="on"
discordwebhook="https://discordapp.com/api/webhooks/xxxx/xxxx"
```

参照: https://docs.linuxgsm.com/alerts/discord

## 実行中のコンテナに入る

```bash
docker compose exec server /bin/bash
# root でログインされるので、sdtdserver ユーザーに変更する
su - sdtdserver

# Linux GSMのコマンドが実行可能になる
./sdtdserver details
```

## Thanks
[Docker-7DaysToDie](https://github.com/vinanrra/Docker-7DaysToDie)
