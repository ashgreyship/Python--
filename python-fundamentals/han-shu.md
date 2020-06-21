# 函数

## 缺省值

### 例子

```python
def sumdata （a,b,c=2）:
    return (a+b)**c
sumdata(2,3)
#输出 25
#c为缺省值（默认值），如果第三个参数没有设置，则使用默认值
```

### 错误写法

```python
def sumdata （a=2,b,c):
    return (a+b)**c
sumdata(2,3)
#缺省值不能写在非缺省值前面
```

有缺省值的参数必须位于无缺省值的参数的后面。

可以有超过一个缺省值。

## 返回值

可以有多个返回值。当有多个返回值，他们以元祖`tuple`形式返回。

## 内置函数

* print\( \)
* int\( \) : 转换字符串形式的整数，或者浮点型的小数。但是不能转换字符串形式的小数。
* str\( \)
* float\( \)
* input\( \)

## 方法

* strip\(\) 去除字符串前后的特定字符
* count\(\) 统计某个字出现在字符串的次数
* join\(\) 将字符连接起来

## 函数和方法区别

函数：通过“函数名（）”的方式进行调用。

```python
class Foo(object):

    def func(self):
        pass

#实例化
obj = Foo()

# 执行方式一:调用的func是方法
obj.func() #func 方法

# 执行方式二：调用的func是函数
Foo.func(123) # 函数
```



