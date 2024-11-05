---
typora-root-url: ./
---

### 特性 && Pythonic

- `__new__` 与 `__init__` 区别

  - `__new__` 在创建一个新对象时调用，通常用于控制实例化过程。在 `__init__` 之前调用。如果 `__new__` 没有返回一个类的实例，`__init__` 就不会被调用

  - `__init__` 用于设置对象的初始状态（属性或其他初始化逻辑）

    ![image-20241031152719164](/img/image-20241031152719164.png)

- `@property` 修饰符

  - 用于将一个方法转换为只读属性，使其可以像属性一样访问，而不需要显式调用方法

    <img src="/img/image-20241031164023002.png" alt="image-20241031164023002" style="zoom:50%;" />

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

- generator 

  生成器函数是一种特殊类型的函数(包含 `yield` 语句的函数即为生成器函数)，它返回一个生成器对象，可以用于逐步生成一系列值，而不是一次性返回一个单独的值。生成器在执行过程中可以暂停和恢复，从而提供了一种更高效的方式来处理大量数据或无限序列。

  - 生成器的 `send` 方法

    用于向生成器发送一个值，同时恢复生成器的执行。与直接调用 `next` 方法不同，`send` 方法允许在恢复生成器执行时传递一个值，生成器可以通过 `yield` 表达式接收这个值。

    ```python
    # 生成器函数
    def main():
        x = 0
        for _ in range(10):
            b = yield read, ()  # 接受 send 传递过来的参数
            x = x * 2 + b
    
        sys_write(f'x = {x:010b}b')
    
    def step(self):
                '''
                Resume the process with OS-written return value,
                until the next system call is issued.
                '''
                syscall, args, *_ = self._func.send(self.retval) # 向生成器函数传递 retval 变量
                self.retval = None
                return syscall, args
    ```

    

  - `yield`

    当生成器函数执行到 `yield` 语句时，它会暂停执行，并返回 `yield` 关键字后面的值。当生成器的 `next()` 方法被调用时，函数从暂停的地方恢复执行，直到遇到下一个 `yield` 语句或函数结束


### 三方库/内置库当中的 trick

- `urllib.parse` 当中的 `urlencode`

  用于将字典或包含键值对的可迭代对象转换为 URL 编码的查询字符串。`doseq` 参数是 `urlencode` 函数的一个布尔值参数，用于控制是否对相同的键进行序列化。

  当 `doseq` 参数被设置为 `True` 时，表示如果字典中的某个键对应的值是一个列表或元组，那么这个键会被序列化成多个相同的键，每个键都对应列表或元组中的一个值。

  ```python
  query_string = urlencode({
              'authenticity_token': token,
              'user[email][]': [self.target, self.evil]
          }, doseq=True)
  ```

- fileinput 库

  支持将命令行的输出通过管道传递给该脚本、 重定向文件到该脚本，或在命令行中传递一个文件名或文件名列表给该脚本

  ```python
  stdin = fileinput.input()
  # 可以直接解析输入
  exec(fileinput.input())
  ```

  传递方式如下：

  ```python
  ls | ./filein.py
  ```

  

### 参考

- [Python 语言基础 - SAST skill docs (net9.org)](https://docs.net9.org/languages/python/#_15)

- [CVE-2023-7028/CVE-2023-7028.py at main · Vozec/CVE-2023-7028 (github.com)](https://github.com/Vozec/CVE-2023-7028/blob/main/CVE-2023-7028.py)

- https://jyywiki.cn/os-demos/introduction/os-model/"