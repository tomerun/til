# anacondaを使う

## ダウンロード・インストール

https://www.continuum.io/downloads から

## 最新の状態に更新

```
$ conda update conda
```

environmentをrootにしておかないと動かない？

## environmentを作る

名前とインストールしたいパッケージを指定して環境を作る

次の例だと、kaggleという名前の環境を作り、初期状態でscikit-learn（とそれが依存するパッケージ）をインストールする

```
$ conda create --name kaggle scikit-learn
```

## environmentを有効にする

```
$ source activate kaggle
```

Windowsだと `source` は不要

## パッケージをインストールする

```
$ conda install pandas
```

## インストールされているパッケージを列挙する

```
$ conda list
$ conda list -r # パッケージの更新履歴を表示
```

## パッケージを更新する

```
$ conda update パッケージ名
$ conda update --all        # 全パッケージを更新
```

## environmentを列挙する

```
$ conda info -e
```


