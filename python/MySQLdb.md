# MySQLdb

MySQL(MariaDBも)に接続するライブラリ、MySQLdbについて

## connection, cursorのクローズ

connection オブジェクトを with 文に渡したら、cursor オブジェクトが返ってくる

```py
import MySQLdb
with MySQLdb.connect(...) db:
    print(db)
# => <MySQLdb.cursors.Cursor object at 0x10cb91080>
```

これは、Connectionクラスの `__enter__()` ではcursorを作って返しているため。また、 `__exit__()` でconnectionをcloseしているわけでもない。

参照：http://stackoverflow.com/questions/5669878/when-to-close-cursors-using-mysqldb

なので、単にwithを使うだけだとconnectionやcursorがcloseされないままになる。
（cursorのほうは別にcloseする必要はなさそうではあるけど…）

確実にconnectionやcursorの `close()` を呼ぶには、 [contextlib](https://docs.python.org/3/library/contextlib.html) を使って次のようにするとよい。

```py
from contextlib import closing
import MySQLdb
with closing(MySQLdb.connect(...)) as db:
    with closing(db.cursor()) as cursor:
        # cursorを使う
```


