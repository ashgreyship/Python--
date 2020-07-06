# 切片（Slice）

## 定义：

取一个list或tuple的部分元素

`L[n:m:z]`

n 是起始索引 （包含起始索引的值）

m 是终止索引 （不包含终止索引的值）

z 是步长 （步长为负数则从后往前走）

## 例子

```python
L[n:m]
#获取index从n 到m-1的元素

L = ['Michael', 'Sarah', 'Tracy', 'Bob', 'Jack']
L[0:3] 
# 输出：Michael，Sarah，Tracy
L[:3]
#输出：Michael，Sarah，Tracy
#如果第一个index是0,可以省略

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
#['Jack', 'Bob', 'Tracy', 'Sarah']
#从最后一位开始取值，到index为1，不包含index=0

```

