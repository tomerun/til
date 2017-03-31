# Vagrantを使う

参照
* http://techacademy.jp/magazine/6304
* http://ruby-rails.hatenadiary.com/entry/20150719/1437249020

## 導入

VirtualBox, Vagrantを公式サイトからインストール

```
$ mkdir vagrant
$ cd vagrant/
$ vagrant box add centos/7
$ vagrant init centos/7    # カレントディレクトリに `Vagrantfile` ができる
$ vagrant up               # ログの中にアドレスなどが出力される
$ vagrant ssh              # ssh接続
$ vagrant reload           # 再起動
$ vagrant halt             # VM電源OFF
```

"centos/7" の部分は使いたいboxの名前を入れる

デフォルトのパスワードは `vagrant`

## sshでログインできない

初回の `vagrant up` 時に `default: Warning: Authentication failure. Retrying...` という警告が出て、SSHでログインできなくてハマる。

いったんパスワードでログインして、 `chmod 600 ~/.ssh/authorized_keys` する。

※vagrantは、 `vagrant init` 時に鍵ペアを作成してそれを鍵として使う。公開鍵は仮想マシンの `~/.ssh/authorized_keys` に書かれ、秘密鍵はvagrant実行ディレクトリの `.vagrant` 内に保存される。この秘密鍵のパスは `vagrant ssh-config` で確認できる

### scpでvagrant内からホストへファイルをコピー

`vagrant ssh-config` するとSSHのポート番号がわかるので、 `scp -P` で指定する

```
$ vagrant ssh-config
Host default
  HostName 127.0.0.1
  User vagrant
  Port 2201
  (snip)
$ scp -P 2201 vagrant@localhost:path/to/file .
```


## Guest Additions

```
$ vagrant plugin install vagrant-vbguest  # vagrantのプラグインをインストール
$ vagrant vbguest                         # Guest Additionsをインストール・更新
```

プラグインの細かい設定などはここに https://github.com/dotless-de/vagrant-vbguest/blob/master/Readme.md


