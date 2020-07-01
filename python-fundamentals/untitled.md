# 模块与包

### 模块:

其实是一个`.py` 文件

```text
# import 模块名
#模块名.函数名

# from 模块名 import 函数名
#函数名
```

### `__main__` 的定义

```python
#当import 某个模块时，这个模块会被执行一次。
# __name__ 为本文件名字
if __name__ == '__main__':
    print('只有自己执行')
#如果执行的名字不是自己，则if statement不会被执行

print(__name__)
#当本文件执行此行,输出 __main__
#当其他文件调用此文件，输出文件名
```

### 包：

存放着若干个模块的文件夹，有`__init__.py` 文件的文件夹

当你调用包的时候，`__init__.py` 会被自动执行。

```python
#from 包名 import 模块
# 模块名.函数名

# from 包名.模块名 import 函数名
# 函数名

# from 包名.模块名 import 函数名  as alias
# 起一个别名

```

### 库:

标准库，第三方库

### 临时将包加入到默认路径中:

```python
import sys
print(sys.path)
sys.path.append('path')
```

### 永久添加路径:

到python的安装的安装目录，进入 Lib/site-packages, 自己添加一个 XXX.pth 文件。可以往文件里添加路径，每次添加一行。



