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




### 三方库当中的 trick

- `urllib.parse` 当中的 `urlencode`

  用于将字典或包含键值对的可迭代对象转换为 URL 编码的查询字符串。`doseq` 参数是 `urlencode` 函数的一个布尔值参数，用于控制是否对相同的键进行序列化。

  当 `doseq` 参数被设置为 `True` 时，表示如果字典中的某个键对应的值是一个列表或元组，那么这个键会被序列化成多个相同的键，每个键都对应列表或元组中的一个值。

  ```python
  query_string = urlencode({
              'authenticity_token': token,
              'user[email][]': [self.target, self.evil]
          }, doseq=True)
  ```

  

### 参考

- [Python 语言基础 - SAST skill docs (net9.org)](https://docs.net9.org/languages/python/#_15)

- [CVE-2023-7028/CVE-2023-7028.py at main · Vozec/CVE-2023-7028 (github.com)](https://github.com/Vozec/CVE-2023-7028/blob/main/CVE-2023-7028.py)