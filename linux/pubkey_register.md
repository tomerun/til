# Linuxマシンに公開鍵を登録してSSHでパスワード無しでログインできるようにする

CentOS6 のサーバーでやった結果なので、他のディストリビューションでは違いがあるかも

* `~/.ssh/authorized_keys` にローカルの公開鍵を追記
* アクセス許可を変更
  * `chmod 700 ~/.ssh`
  * `chmod 600 ~/.ssh/authorized_keys`
  * これより強くても弱くてもダメらしい
* `/etc/ssh/sshd_config` を変更
  * `#PubkeyAuthentication yes` のコメントを外す
  * パスワードログインを無効化する場合、 `#PasswordAuthentication yes` のコメントを外して `no` にする
    * これをやる前に、一度ログアウトしてSSHでログインできることを確認する。そうしないともしミスっていたらログイン不可能になって詰む
* sshdを再起動
  * `/etc/init.d/sshd restart`


