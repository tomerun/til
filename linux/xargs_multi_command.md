# xargsで複数のコマンドを使う

xargsで処理した結果に対してパイプを使おうとするとうまくいかない。

```
$ echo "123
456" > a.txt
$ echo "abc
def" > b.txt
$ find . -name "*.txt" | xargs rev | tail -n 1
fed # 出力の全体に対してtailが適用されてしまう
```


xargsの `-I` オプションを、shコマンドと組み合わせて使うと良い。

```
$ find . -name "*.txt" | xargs -I {} sh -c "rev {} | tail -n 1"
654
fed
```

`-I` オプションは他にも、入力の文字列をコマンドの末尾ではなく途中に置きたい場合にも使える。

```
$ mkdir dst
$ find . -name "*.txt" | xargs -I {} cp {} dst
$ ls dst
a.txt  b.txt
```

