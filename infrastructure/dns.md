# DNSまわり

## digコマンド

DNSの名前引きの情報を調べるには `dig` コマンドを使う

http://d.hatena.ne.jp/japanrock_pg/20090410/1239355230

関連するソフトウェアとして、DNSサーバーを実装した `BIND` がある

## Aレコード、CNAMEレコード

* Aレコードで、ドメイン名 → IPアドレス の関係を定義
  * IPアドレスは複数書ける
* CNAMEレコードで、ドメイン名の別名を定義
  * つまり、複数のドメインを同じIPアドレスに結び付けられる
  * バーチャルホスト

## Rount53

Rount53は、AWSでネームサーバーを作れるサービス

http://fujiike.hateblo.jp/entry/2015/09/14/191934
