原文链接：[Quickstart tutorial](https://docs.scipy.org/doc/numpy/user/quickstart.html)


## 前提

## 基础

## Shape Manipulation

## 副本和视图
When operating and manipulating arrays, their data is sometimes copied into a new array and sometimes not. `This is often a source of confusion for beginners. There are three c`ases:
当操作arrays时，有时需要将其中的数据复制到新的array，有时不需要这么做。对于初学者来说这是经常造成困扰的原因，下面是三种场景：
- 不需要复制  
  简单的赋值不会创建数组对象的副本。 相反，它使用原始数组的相同id()来访问它。 id()返回Python 对象的通用标识符，类似于 C 中的指针。此外，一个数组的任何变化都反映在另一个数组上。 例如，一个数组的形状改变也会改变另一个数组的形状。
```
>>> a = np.arange(12)
>>> b = a            # no new object is created
>>> b is a           # a and b are two names for the same ndarray object
True
>>> b.shape = 3,4    # changes the shape of a
>>> a.shape
(3, 4)
```
```
>>> def f(x):
...     print(id(x))
...
>>> id(a)                           # id is a unique identifier of an object
148293216
>>> f(a)
148293216
```
- 识图或浅复制
- 深复制