# 闭包

闭包是一个内部函数

闭包可以接受参数

```python
def outer():
    x = 10

    # 在一个内部函数里边，对在外部作用域(但不能是全局作用域)的变量进行引用
    # 那么这个内部函数就被认为是闭包    
    def inner():
        print(x)

    return inner


outer()
f = outer()
f()

```

