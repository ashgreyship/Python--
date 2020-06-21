# 格式化字符串

## 方案一：

`%s`指字符串

`%d`指字符串

```python
info = 'my name is %s, age is %s'%('Mary',22)
#格式化字符串最后，是元祖的形式

info = 'my name is %s, age is %5s'%('Mary',22)
#5s表示至少要补满5位
#my name is Mary, age is    22

info = 'my name is %s, age is %5s'%('MaryMary',22)
#如果值比设置的位数多，不受影响

```

`%f`指浮点数

```python
'%.3f'%3.1415926
#保留三位小数
'%6.3f'%3.1415926
#选择最大位数
```

`%x`指十六进制

## 方案二：

```python
print('My name is {}, I am {} years old'.format('Tom',39))

print('My name is {:6}, I am {:6} years old'.format('Tom',39))
#字符串至少要六位，
#字符串为左对齐，数字为右对齐
#长度不够用空格代替。

print('My name is {:<6}, I am {:<6} years old'.format('Tom',39))
#如果要强制左对齐，需要写<

print('My name is {:>6}, I am {:>6} years old'.format('Tom',39))
#如果要强制右对齐，需要写>

print('My name is {:^6}, I am {:^6} years old'.format('Tom',39))
#如果要强制居中对齐，需要写^
```



