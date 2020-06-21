# 切片（Slice）

#### 切片：

取一个list或tuple的部分元素

```python
L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
L[0:3] 
# 输出：Michael，Sarah，Tracy
L[:3]
#输出：Michael，Sarah，Tracy
#如果第一个index是0,可以省略

L[n:m]
#获取index从n 到m-1的元素

L[-2:]
#输出：Bob,Jack
#从倒数第二个到倒数第一个
L[-2:-1]
#输出：Bob
#获取倒数第二个（不包括倒数第一个）

L[:4:2]
#输出：Michael，Tracy
#获取前4个，每两个取一个元素

L[::2]
#['Michael', 'Tracy', 'Jack']
#所有数字，每两个取一个

L[5:0:-1]


```



