# 循环

## For 循环

```python
sumdata = 0
for i in range(1,101):
    # i从1开始，到101结束，实际只计算到100
    sumdata = sumdata+i
    #break
else:
    print(sumdata)
```

`for` 后面也可以带 `else`, 如果循环正常执行结束而没有意外中断，则执行一次`else`中的语句。

`Break` 属于中断循环。`continue`不是中断循环。







