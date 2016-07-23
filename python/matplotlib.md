# matplotlibを使う

## 設定

matplotlibrc というファイルに設定が書かれている。

今読み込んでいる設定ファイルは、 `matplotlib.matplotlib_fname()` でわかる。

自分の環境では `c:\Users\%USER_NAME%\Anaconda3\envs\kaggle\Lib\site-packages\matplotlib\mpl-data\matplotlibrc` だった（Anacondaでkaggleという名前のenvironmentを作っている）

コード中からは、 `matplotlib.rcParams` という dictionary で参照できる。

値を変更するには、 `matplotlib.rc()` を使うと良い。

```python
import matplotlib as mpl
mpl.rc('lines', linewidth=2, color='r')
```

`matplotlib.rcdefaults()` を呼ぶとデフォルト値に戻る。



