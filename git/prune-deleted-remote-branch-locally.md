# リモートで削除されたブランチが手元に残っているのをまとめて削除する

リモート（たとえば、GitHub上）でブランチを削除しても、以前にpullしたローカルにはリモートブランチとして残ったままになる。

```
$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/boot_agent
  remotes/origin/boot_test
  remotes/origin/daily_test
  remotes/origin/easy_test
  remotes/origin/fw_update_complete
  remotes/origin/graph
  remotes/origin/master
  remotes/origin/poweroff_wait
  remotes/origin/temp
```

リモートで削除済みのブランチを一括で削除するには、 `git fetch` や `git pull` に `--prune` オプションをつけると良い。

```
$ git pull --prune
From github.fixstars.com:STEP/pinot-test
 x [deleted]         (none)     -> origin/boot_agent
 x [deleted]         (none)     -> origin/boot_test
 x [deleted]         (none)     -> origin/daily_test
 x [deleted]         (none)     -> origin/easy_test
 x [deleted]         (none)     -> origin/fw_update_complete
 x [deleted]         (none)     -> origin/poweroff_wait
 x [deleted]         (none)     -> origin/temp
Already up-to-date.

$ git branch -a
* master
  remotes/origin/HEAD -> origin/master
  remotes/origin/graph
  remotes/origin/master
```



