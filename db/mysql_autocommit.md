# MySQL（InnoDB）でのautocommit

InnoDBでは、デフォルトで自動コミットモードがONになっている。

## OFFにするには

OFFにするには、 `autocommit` 変数を0にする。この変数はセッションごとに独立。
```
SET autocommit=0;
``` 

## 振る舞い

### ONの場合

自動コミットモードがONの場合、単一の各SQLがトランザクションとなる。

ただし、 `START TRANSACTION` または `BEGIN` 文を実行した場合は例外で、`COMMIT` または `ROLLBACK` を実行するまでがトランサクションになる。

### OFFの場合

自動コミットモードがOFFの場合、SQL文を実行すると新たなトランザクションの開始になり、`COMMIT` または `ROLLBACK` の実行により閉じられる。
`START TRANSACTION` または `BEGIN` の実行は影響なし。

`SELECT` 文だけでもトランザクションが開始する。 `COMMIT` または `ROLLBACK` しないとトランザクション掴みっぱなしになってマズい。
これを防ぐため、Webシステムではセッションの最後に `ROLLBACK` を常に発行する、といった対処がされることがある。


参照：
- https://dev.mysql.com/doc/refman/5.6/ja/commit.html
- https://open-groove.net/mysql/autocommit/
- http://atsuizo.hatenadiary.jp/entry/2016/12/05/000000

