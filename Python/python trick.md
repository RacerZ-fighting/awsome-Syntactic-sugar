### 特性 && Pythonic

- 自动生成元组与解包

  ```python
  # 场景 1: 自动生成元组
  a = 1
  b = 2
  a, b = b, a # 自动生成了 Tuple 并交换次序，不需中间变量
  # 场景 2: 传参解包
  xlim = [15000, 40000]
  plt.xlim(*xlim)
  ```

  





### 参考

- [Python 语言基础 - SAST skill docs (net9.org)](https://docs.net9.org/languages/python/#_15)