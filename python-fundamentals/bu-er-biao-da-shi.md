# 布尔表达式

### AND

`and`优先于`or`

```text
print（1>3 and "ABCD"）
```

输出值为false

```text
print（1<3 and "ABCD"）
```

输出值为

```text
ABCD
```

#### 原因：当使用`and`的时候，

如果前面是true，后面继续执行。

如果前面是false，后面不执行。

### OR

```text
print(1>3 or 'ABCD')
```

输出 ABCD。

如果前面是true，后面不执行。

如果前面是false，后面继续判断。

### NOT

`not` 优先于`and`, `or`



