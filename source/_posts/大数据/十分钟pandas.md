原文链接:[10 Minutes to pandas](http://pandas.pydata.org/pandas-docs/stable/10min.html)

这是一个针对新手的pandas简短介绍，如果想阅读更详细的手册请参考[Cookbook](http://pandas.pydata.org/pandas-docs/stable/cookbook.html#cookbook)

我们通过下面的方法导入相关模块
```python
In [1]: import pandas as pd

In [2]: import numpy as np

In [3]: import matplotlib.pyplot as plt
```

### 创建对象
参考[数据结构介绍部分](http://pandas.pydata.org/pandas-docs/stable/dsintro.html#dsintro)















### Misc
设置最多可显示的列数。下面的代码设置最多显示100列。

pd.options.display.max_columns = 100


也可以取消限制，比如设置为None。

pd.options.display.max_columns = None