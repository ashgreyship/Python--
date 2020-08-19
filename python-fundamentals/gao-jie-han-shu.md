# 高阶函数

```python
def foo():
    print('abc')


# 函数名也是变量，可以被复赋值给其他变量
f = foo

f()


def bar(x):
    x()


# 函数名可以作为参数传递
bar(foo)


# 函数名可以作为返回值
def wrapper():
    def inner():
        print("我是inner")

    return inner


wrapper()()
```

