# Mongo DB tutorial

## 基本的な構成

||version|
|----|----|
|OS|Ubuntu 22.04|
|ホストマシン|docker on WSL2|
|Mongo DB|v6.0.6|
|mongosh|v1.9.1|

<!-- ## インストール -->
`.docker/mongodb/Dockerfile`をそのまま使用する場合はこの手順はスキップ。
次の立ち上げを参照してください。

1. 基本的には公式のドキュメント通りに進める。

https://www.mongodb.com/docs/v4.4/tutorial/install-mongodb-on-ubuntu/#run-mongodb-community-edition

2. mongod (Mongo DB server daemon) の起動時にエラーが出るため、別の方法で起動。

```sh
$ sudo service mongod start
mongod: unrecognized service.
```

```sh
$ mkdir ~/data/db
$ mongod --dbpath ~/data/db
{"t":{"$date":"2023-06-04T05:48:50.752+00:00"},"s":"I",  "c":"NETWORK",
.
.
```

3. 27017 portでプロセスが起動しています。

## dockerコンテナ立ち上げ
コンテナを使用していない場合はこちらの手順は不要です。
インストールの2ですでにサーバーは立ち上がっています。

```sh
$ docker build -t mongodb -f .docker/mongodb/Dockerfile ./mongodb
$ docker run mongodb
```

## mongoshの起動

```sh
$ docker exec -it nosql-mongodb-1 mongosh
```

or コンテナを使わずインストールしている場合

```sh
$ mongosh
```