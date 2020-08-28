# 调用外部程序

## 使用 OS

`os.system`是阻塞式调用

函数有返回值，返回值为 0 代表外部程序调用成功

函数有返回值，返回值为 1 代表外部程序调用失败

```python
import os

# 阻塞式调用，调用的外部程序退出之前，python程序会一直等在这里
# 直到外部程序退出，才会接着往下运行
ret = os.system('ps')
print(ret)
os.getpid()
print("after")
```

## 使用 subprocess

`subprocess.popen` 非阻塞式调用

调用 wait 方法可变为阻塞式调用

```python
import subprocess

# 执行指定的命令
# 阻塞式调用
# 执行指定命令，并将结果以字符串的形式返回
ret = subprocess.check_output('ls')
print(ret.decode('utf'))

# 非阻塞式调用
child = subprocess.Popen("ls", stdout=subprocess.PIPE)
child.wait()

output, err = child.communicate()
print(output.decode("utf-8"))
print(err)
```



