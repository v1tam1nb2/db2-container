# db2-container
DB2コンテナのサンプル

## コンテナ起動

```shell
docker compose up -d
```

## サンプルデータの投入

```shell
# コンテナ内に入る
docker exec -it db2 bash
# パスを通す
export PATH=/database/config/db2inst1/sqllib/bin/:$PATH
# データベースに接続
db2 connect to USERDB user db2inst1 using password

# テーブル作成
db2 -tvf /var/custom/sql/create_users.sql
# データのインサート
db2 import from /var/custom/data/insert.csv of del insert into users

# Terminate
db2 terminate

# コンテナから出る
exit
```

## サンプルデータの確認

```shell
# db2ins1ユーザーでコンテナに入る
docker exec -it db2 bash -c "su - db2inst1"

# データベースに接続
db2 connect to userdb
# selectの実行
db2 "select * from users"

# Terminate
db2 terminate

# コンテナから出る
exit
```

セレクト結果

```
[db2inst1@9b483c1926bf ~]$ db2 "select * from users"

ID                                   NAME                                     MAIL                                                                                                 PASSWORD                       CREATED_AT                 UPDATED_AT
------------------------------------ ---------------------------------------- ---------------------------------------------------------------------------------------------------- ------------------------------ -------------------------- --------------------------
test                                 test                                     test@test.com                                                                                        testtest                       2025-01-02-11.00.00.000000 2025-01-02-11.00.00.000000
sample                               sample                                   sample@sample.com                                                                                    samplesample                   2025-01-11-11.00.00.000000 2025-01-11-11.00.00.000000

  2 record(s) selected.

[db2inst1@9b483c1926bf ~]$
```
