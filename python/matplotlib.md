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


## プロットする

`matplotlib.pyplot.plot()` を使う。

渡すデータは内部的に numpy.array に変換されている。

詳しくは [リファレンス](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.plot) を参照。

キーワード引数で設定できるプロパティは [Line2D](http://matplotlib.org/api/lines_api.html#matplotlib.lines.Line2D) のもの。

```python
import matplotlib.pyplot as plt
plt.plot([1,2,3,4],[1,4,9,16], 'r-', label='data1')  # plot(xs, ys, fmt, other_properties)
plt.plot([2,3,4,5],[1,2,3,4],'b--', label='data2')   # fmtは色とスタイルの組み合わせでできている
plt.axis([0, 6, 0, 20]) # axis(xmin, xmax, ymin, ymax)
plt.xlabel('input')
plt.ylabel('output')
plt.legend()
plt.show()
```

plot関数の戻り値に、Line2Dオブジェクト（またはそのリスト）が返される。
それを使って線のプロパティを指定することもできる。

```python
line, = plt.plot(x, y, '-')
line.set_antialiased(False)
plt.show()
```

## 複数のプロットを作る

[`pyplot.subplot()`](http://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplothttp://matplotlib.org/api/pyplot_api.html#matplotlib.pyplot.subplot) を使う。

matplotlibにはfigureとaxesという概念がある。figureの中に複数のaxesが含まれる。






