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


## 前にチェックアウトしていたブランチに戻る

'-' が1つ前のブランチを表すことになり、 `git checkout -` で前にチェックアウトしていたブランチに戻れる。

git-checkoutのヘルプより
```
           As a special case, the "@{-N}" syntax for the N-th last branch/commit checks out branches
           (instead of detaching). You may also specify - which is synonymous with "@{-1}".
```


