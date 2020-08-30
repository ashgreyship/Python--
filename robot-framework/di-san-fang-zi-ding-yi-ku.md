# 第三方自定义库

## 自定义库

```python
def get_type(obj):
    return str(type(obj))[8:-2]


def print_value(*args, **kwargs):
    for arg in args:
        print(arg)
    for k in kwargs:
        print(kwargs[k])


if __name__ == '__main__':
    for i in range(0, 100, 4):
        print(i)
    pass
    # print(get_type([1, 2, 3]))
```

## 引用自定义库

```python
*** Settings ***
Library  testlib.py

*** Test Cases ***
case1
    ${list}  set variable  a  b  c
    ${type}  get type  ${list}
    log to console  ${type}
```



