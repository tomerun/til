# jupyter notebook を使う

## ダウンロード・インストール

Anacondaを入れるとデフォルトで入っている
それ以外ならpipでインストールするとか

## 起動

```
$ jupyter notebook --port 8889
```

とやるとブラウザでnotebookの画面が開く
ポートはデフォルトでは8888だが、手元のWindows10環境ではそれだと動かなかった
参照： http://stackoverflow.com/questions/35486586/jupyter-with-anaconda-on-windows-will-not-run-cells

適当にポチポチやるとコマンドを打ち込める画面が開く
Shift+Enter で打ち込んだコマンドが実行される

ここでファイルを保存するとnotebookファイル（*.ipynb）になってあとから続きをできる

## matplotlibのグラフをインラインで表示する

`%matplotlib inline` を実行しておくと、matplotlibの画像がnotebook上で表示されるようになる。

グラフのスタイルは、 `plt.style.use(スタイル名)` で変更できる。
利用できるスタイルの一覧は `plt.style.available` で


