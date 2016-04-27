# git diffで変更があったファイルのdiffだけを表示させる

`git diff` では、追加・削除されたファイルがあるとその内容も全て差分として表示されるが、これは邪魔なことが多い。

`--diff-filter` オプションを使うと、表示するファイルの種類を限定できる。変更したファイルだけを表示したい場合は `git diff --diff-filter=M` など。

git diff --help より
```
--diff-filter=[(A|C|D|M|R|T|U|X|B)...[*]]
    Select only files that are Added (A), Copied (C), Deleted (D), Modified (M), Renamed (R), have their type (i.e. regular file, symlink, submodule, ...)
    changed (T), are Unmerged (U), are Unknown (X), or have had their pairing Broken (B). Any combination of the filter characters (including none) can be
    used. When * (All-or-none) is added to the combination, all paths are selected if there is any file that matches other criteria in the comparison; if
    there is no file that matches other criteria, nothing is selected.
```
