# curl

HTTPアクセスのちょっとしたテストはcurlでできるようになっときたいですね

## リクエストメソッド

`-X` で指定する。デフォルトはGET。

```
$ curl -X POST https://...
```

## POSTのフォームデータ

`-d` で指定する。URLエンコードが必要な場合は `--data-urlencode`

```
$ curl -X POST -d "key1=abc" --data-urlencode "key2=あいう" https://...
```

マルチパートの場合はまた違うはずだけどまだ使う機会がないので調べてない

## Cookie

`-c` でファイルパスを指定すると、 `Set-Cookie` で指定された値がそのファイルに保存される。

以降、 `-b` でそのファイルを指定するとCookieを設定してリクエストされる

```
$ curl -c /path/to/cookiejar https://xxx...
$ curl -b /path/to/cookiejar https://yyy...
```

-b では 'キー=値' の形でCookieの値を直接書くことも可能。

## 証明書の警告を無視

`-k`
