# 数値シーケンスを作るためのコマンド

## seq

```
$ seq 1 3  # start, end
1
2
3
$ seq 3 1
3
2
1
$ seq 0 0.2 1  # start, incr, end
0
0.2
0.4
0.6
0.8
1
$ seq -f %.2f 0 0.2 1  # printf形式でフォーマット
0.00
0.20
0.40
0.60
0.80
1.00
$ seq -s , -t ] 1 3  # separator, terminator
1,2,3,]
```

## shuf

ランダムな数値シーケンスを作る。

Macの場合はgshuf、coreutilsに入っている

```
$ shuf -i 1-5  # 範囲
2
4
3
5
1
$ shuf -i 1-100 -n 5  # 出力行数を制限
8
80
72
11
31
$ shuf -i 1-5 -n 8 -r  # 復元抽出（-n を指定しないと無限に出力される）
1
1
2
4
5
5
3
2
```

