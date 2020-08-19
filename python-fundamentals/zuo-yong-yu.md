# 作用域



* L （Local） 局部作用域
* E （Enclosing） 嵌套作用域
* G （Global） 全局作用域
* B （Built-in） 内建作用域

以 _**L –&gt; E –&gt; G –&gt;B**_ 的规则查找，即：在局部找不到，便会去局部外的局部找（例如闭包），再找不到就会去全局找，再者去内建中找。

Python除了**`def/class/lambda`** 外，其他如: **`if/elif/else/ try/except for/while`**并不能改变其作用域。定义在他们之内的变量，外部还是可以访问。

```python
lVar = 100           #G
 
def test_scope():
    enclosingVar = 200    #E
    def func():
        localVar = 300    #L
print (__name__)            #B
```

