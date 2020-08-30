# 常用的变量

```python
*** Settings ***
Library  SeleniumLibrary

*** Test Cases ***
set variable string
    ${var}  set variable  2020  hello  world
    log to console  ${var}

set variable integer
    ${var}  set variable  ${2020}
    log to console  ${var}

set variable integer-keyword
    ${var}  convert to integer   2020
    log to console  ${var}

log variable
    log  记录日志
    #sleep  3
    log to console  记录日志2  输出日志到控制台

assert variable
    ${list}  set variable  a  b  c
    # 此时为 list 和string比较
    #should be equal  ${list}  ['a','b','c']
    should be equal as strings  ${list}  ['a', 'b', 'c']

    should not be equal  ${list}  ['a','b','c']

assert variable 2
    ${actual}  set variable  robot
     # 如果关键字参数不是python表达式，传参用传统形式 ${var}
    should be true  '${actual}' in 'robot framework'
    should be true  $actual in 'robot framework'

    log to console  $actual


```

