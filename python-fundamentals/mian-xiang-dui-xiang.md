# 面向对象

例子:

```python
class Rectangle:
    def __init__(self, chang, kuan):
        self.chang = chang
        self.kuan = kuan

    def length(self):
        return (self.chang + self.kuan) * 2
        
cfx = Rectangle(6,4)
print(cfx.length())
print(cfx.dict)
```

