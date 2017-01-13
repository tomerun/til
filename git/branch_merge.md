# ブランチ・マージ関連

## ブランチ名を変更する

`git branch -m (旧ブランチ名) 新ブランチ名`
旧ブランチ名を省略すると現ブランチが対象になる

git-branchのヘルプより
```
       -m, --move
           Move/rename a branch and the corresponding reflog.
```

## あるブランチで変更されたファイルを他のブランチへ持ってくる

mergeだと全ファイルのマージになってしまうが、特定のファイルだけを持ってきたい場合。

`git checkout 元ブランチ名 -- ファイルパス` で現ブランチへ取得できる。


