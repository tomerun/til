# tmux

tmuxを使えるようにしておこうかと

## インストール

* `brew install tmux`
* `brew install reattach-to-user-namespace`
  * これはクリップボードをOSと連携させるため


## 設定

デフォルトのprefixである `Ctrl-b` はカーソル移動とバッティングするので `Ctrl-g` に変えておく。

```
set-option -g prefix C-g
unbind-key C-b
bind-key C-g send-prefix
```

マウススクロールでコピーモードにする（というか、各ペインの内容がスクロールされるようにする）

```
set-option -g mouse on
```

Escキーがすぐ反応するようにする

```
set -s escape-time 0
```

tmuxのコピーモードではtmux内だけのバッファにコピーされてしまうのでOSのクリップボードにコピーされるようにする

```
set-option -g default-command "exec reattach-to-user-namespace -l $SHELL"
bind-key -T copy-mode M-w send-keys -X copy-pipe 'reattach-to-user-namespace pbcopy'
bind-key -T copy-mode C-w send-keys -X copy-pipe 'reattach-to-user-namespace pbcopy'
```

メタキーとしてOptionを使えるよう、ターミナルの設定で https://blog.catatsuy.org/a/243 にあるように `メタキーとして option キーを使用` のチェックを入れた

コピーモードのキーバインドはどっちにしようかなあ、まずはデフォルトのEmacs風にした


## コマンド

* `tmux a`
  * セッションにアタッチ
* `tmux ls`
  * セッションをリスト
* `tmux kill-session`
  * セッションを終了

tmux内で

* `prefix s`
  * セッションの一覧
* `prefix d`
  * セッションをデタッチ
* `prefix w`
  * ウィンドウの一覧
* `prefix [0-9np]`
  * ウィンドウ移動
* `prefix c`
  * ウィンドウ作成
* `prefix ["%]`
  * ペインの分割
* `prefix [o↑→↓←]`
  * ペインの移動
* `prefix x`
  * ペインの削除
* `prefix [`
  * コピーモードに移行
  * コピーモード内では、Emacs風キーバインドでカーソル移動・スペースでコピー開始位置の指定・Ctrl-w でコピー
* `prefix ]`
  * ペースト
  * OSのクリップボードと連携させたので普通に `Command + V` でもペーストできる

ペインのサイズ変更のショートカットがうまく動かないのでなんとかせねば
このへんかな http://peccu.hatenablog.com/entry/2015/08/15/000000

