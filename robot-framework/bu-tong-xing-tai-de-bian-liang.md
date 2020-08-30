# 不同形态的变量

```python
*** Settings ***
Library  testlib.py

*** Test Cases ***
列表形态变量
    # @{list} --展开列表内的元素 @ 相当于拆包列表
    ${list}  set variable  a  b  c
    print value  @{list}
    log to console  ${list[1]}
    log to console  ${list}[0]

字典形态的变量
    #&{dict} --展开字典内的元素，作为多个参数传递 -- @ 相当于拆包字典
    ${dict}  create dictionary  a=1  b=2  c=3
    log to console  ${dict}
    log to console  获取字典中的第一个值
    log to console  ${dict}[a]
```

