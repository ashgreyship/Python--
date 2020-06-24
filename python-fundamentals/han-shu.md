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
Foo.func(123) # 函数用于
```

## 作用域

### 全局变量

```python
a = 0
def fun1(c, d):
    global e
    e = 3
    # 声明 e 为全局变量，如果不声明，则e为局部变量
    return (c + d) * e

print(fun1(3, 6))
print(a)
print(e)

```

### 缺省值进阶

```python
#如果需要修改每个参数之间的间隔符，可以加入 sep = '自定义参数'
print ('a','b','c', sep = '|||||')
#output: a|||||b|||||c

#如果需要修改每次打印后自动换行，可以加入 end = '自定义的结束符'
print('a','b','c',end='')
print('a','b','c')
#output: a b ca b c

#如果需要将print 的内容输入到文件中，可以加入 file = '文件'
with open ('path','w+') as ifile:
    print('a','b','c',end='',file=ifile)

#
import time
for i in range(0,101):
    print('\r', f'当前进度{i}%',end='',flush = True)
    time.sleep(0.1)
 
       
import time

print('上课倒计时：')
for i in range(10, -1, -1):
    print('\r', f'上课倒计时{i}秒', end='', flush=True)
    time.sleep(1)

```

### 可变数量的参数（位置参数）

允许在传递实参时候，传输不定数量的参数

```python
def fun(a,b,*args):
    print(a,b,args)
fun(1,2,345,678,90)

#output: 1 2 (345, 678, 90)
#以元祖输出

#可以搭配缺省值
def fun(a,b,*args,c=0):
    print(a,b,args)
fun(1,2,345,678,90,c=90)
```

### 关键字参数

参数位置永远在关键词参数的前面

```python
def func (a,b, *args,**kwargs):
    print (a,b,args,kwargs)
func(1,2,3,4,5,6,7,8,qqq='b')
```

