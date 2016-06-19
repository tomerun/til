# anacondaを使う

## ダウンロード・インストール

https://www.continuum.io/downloads から

## 最新の状態に更新

```
$ conda update conda
```

## environmentを作る

名前とインストールしたいライブラリを指定して環境を作る

次の例だと、kaggleという名前の環境を作り、初期状態でscikit-learn（とそれが依存するライブラリ）をインストールする

```
$ conda create --name kaggle scikit-learn
```

## environmentを有効にする

```
$ source activate kaggle
```

Windowsだと `source` は不要

## ライブラリをインストールする

```
$ conda install pandas
```

## インストールされているライブラリを列挙する

```
$ conda list
$ conda list -r # ライブラリの更新履歴を表示
```

## environmentを列挙する

```
$ conda info -e
```


