# 异常

```python
try:
    a = 0
    print(100 / a)
except ZeroDivisionError:
    print('0 不能作为分母')
else:
    print('程序没有出现问题')
finally:
    print('一定会执行')
```

## 异常

`NameError` 未定义的异常

`ZeroDivisionError` 分母为0

`SyntaxError` 语法异常

`IndexError` 下标异常

`IOError` 输入输出异常

## Exception

很多异常的父类



