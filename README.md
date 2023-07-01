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

## CRUD

### READ

## 用語

- Database
データベース。SQLでいうところのデータベースに相当する。

- Collection
SQLでいうところのテーブルに相当する。

- Record
SQLでいうところのレコードに相当する。

## コマンド

- databaseのリスト。SQLと同じ。

 ```mongosh
> show dbs
```

- 使用するdatabaseの選択
まだ存在していないdatabaseでもOK

```mongosh
> use flightData
```

- コレクションの作成
同じくまだ存在していないコレクションでもOK

```mongosh
> db.flightData.insertOne({})
```

### update

```
> use carRental
switched to db carRental

> db.companies.insertOne({})
{
  acknowledged: true,
  insertedId: ObjectId("64a02696ece380d2c42f0989")
}

> db.companies.updateOne()db.companies.updateOne({_id: ObjectId("64a0266aece380d2c42f0988")}, {$set: {"name": "fumi-rental"}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 1,
  modifiedCount: 1,
  upsertedCount: 0
}

> db.companies.find()
[
  { _id: ObjectId("64a0266aece380d2c42f0988"), name: 'fumi-rental' }
]

> db.companies.insertOne({})
{
  acknowledged: true,
  insertedId: ObjectId("64a02696ece380d2c42f0989")
}

> db.companies.updateMany({}, {$set: {established: "2023-01-01"}})
{
  acknowledged: true,
  insertedId: null,
  matchedCount: 2,
  modifiedCount: 1,
  upsertedCount: 0
}

> db.companies.find()
[
  {
    _id: ObjectId("64a0266aece380d2c42f0988"),
    name: 'fumi-rental',
    established: '2023-01-01'
  },
  {
    _id: ObjectId("64a02696ece380d2c42f0989"),
    established: '2023-01-01'
  }
]
```