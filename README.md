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

## 用語

- Database
データベース。SQLでいうところのデータベースに相当する。

- Collection
SQLでいうところのテーブルに相当する。

- Record
SQLでいうところのレコードに相当する。

## CRUD

### CREATE

- Recordの作成

```mongosh
> db.flights.insertOne({})
{
  acknowledged: true,
  insertedId: ObjectId("647d6515c8bd57d7d93e8747")
}
```

- Collectionの作成
同じくまだ存在していないCollectionでもOK。recordを作成すると自動的にCollectionも作成される。

- databaseの作成 (使用するdatabaseの選択)
まだ存在していないdatabaseでもOK。存在しないdatabaseを選択した場合自動的に作成される。

```mongosh
> use flightData
```

### READ

- databaseのリスト。SQLと同じ。

 ```mongosh
> show dbs
```

- databaseに存在するのリスト

```mongosh
> show collections
```

- collectionに存在するrecordのリスト

オプションなし
```mongosh
> db.flights.find()
[
  { _id: ObjectId("647d6515c8bd57d7d93e8747") },
  {
    _id: ObjectId("647d6535c8bd57d7d93e8748"),
    departureAirport: 'OKI',
    arrivalAirport: 'HND'
  },
  {
    _id: ObjectId("647d6545c8bd57d7d93e8749"),
    departureAirport: 'OKI',
    arrivalAirport: 'HND',
    distance: 1200,
    domestic: true
  }
]
```
綺麗に出力
```mongosh
> db.flights.find().pretty()
[
  { _id: ObjectId("647d6515c8bd57d7d93e8747") },
  {
    _id: ObjectId("647d6535c8bd57d7d93e8748"),
    departureAirport: 'OKI',
    arrivalAirport: 'HND'
  },
  {
    _id: ObjectId("647d6545c8bd57d7d93e8749"),
    departureAirport: 'OKI',
    arrivalAirport: 'HND',
    distance: 1200,
    domestic: true
  }
]
```

### WRITE

- レコードを一つ作成

```mongosh
> 