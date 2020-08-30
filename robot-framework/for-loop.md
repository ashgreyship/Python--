# for loop

```python
*** Test Cases ***
循环1
    ${list}  create list  a  b  c  d
    FOR  ${one}  IN  @{list}
    # rf中没有缩进
    log to console  ${one}
    #结束循环
    END

循环2-IN-RANGE
    # IN RANGE 需要大写 并且只能空一格
    FOR  ${one}  IN RANGE  100
        log to console  ${one}
    END

循环2-Start-end
    FOR  ${one}  IN RANGE  50  100
    log to console  ${one}
    END

循环3-步长模式
    FOR  ${one}  IN RANGE  50  100  2
    log to console  ${one}
    END
```

