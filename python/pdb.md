# pdb

Python標準のコマンドラインデバッガ、[pdb](https://docs.python.org/3/library/pdb.html) について


## コマンド（よく使いそうなもの）

* w
  * スタックトレースを表示
* p [expression]
  * 式を評価して表示
  * pだけではなくppもある
* l
  * 現在位置の周辺ソースコードを表示
* s
  * ステップイン
* n
  * ステップオーバー
* r
  * ステップアウト
* c
  * ブレークポイントにヒットするまで実行
* b
  * ブレークポイントを設定
  * `b [filename:]lineno`
    * filenameのlineno行目に設定
  * `b function`
    * 現在のファイルの関数functionの先頭に設定
  * 2つ目の引数に式を指定することで、条件付きブレークポイントにできる


## 使い方

* 起動時から
  * `pdb.run(statement)` で、statementに指定したものをpdbで実行する
* post-mortemデバッグ
  * `pdb.pm()` を呼ぶと、 `sys.last_traceback` に設定されているスタックトレースを元にpdbを起動する
* ハードコーディング
  * `pdb.set_trace()` をソースコード内に書いておくと、その行を実行するところでpdbが起動する

