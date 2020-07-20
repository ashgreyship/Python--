# 正则表达式 Regular Expression

```python
import re

str1 = 'songqin'
# . 表示任意1位字符，除了换行符\n和制表符\t
# findall的返回值是一个列表
a = re.findall('.', str1)
print('.: ' + str(a))

# * 表示任意0到n位字符
a = re.findall('s*', str1)
print('s*: ' + str(a))

# .* 贪婪匹配
a = re.findall('s.*', str1)
print('s.*: ' + str(a))

# .* 贪婪匹配
a = re.findall('s.*g', str1)
print('s.*g: ' + str(a))

# .*? 偷懒匹配
a = re.findall('s.*?', str1)
print('s.*?: ' + str(a))

# 匹配s之后到g之前的所有值，包含s和g,如果匹配到就停止
a = re.findall('s.*?g', str1)
print('s.*?g: ' + str(a))

# (.*?) 带上括号之后，就不包含边界值
a = re.findall('so(.*?)in', str1)
print('so(.*?): ' + str(a))

# *和+的区别，+号至少要匹配一位，而*可以是0位或多位
# ？允许偷懒
a = re.findall('so.+?', str1)
print('so.+?: ' + str(a))

a = re.findall('so.*?', str1)
print('so.*?: ' + str(a))

str2 = '<span class="td">共31页，到第</span>'
print(re.findall('<span class="td">共(.+?)页，到第</span>', str2))

str3 = 'abc$de'
# \w表示匹配字母数字下划线
# {}里面的数字表示多个字母数字下划线连续匹配
a = re.findall('\w{2}', str3)
print('\w{2}: ' + str(a))

str4 = '             abc   \n'
# \s 匹配空字符串，以及\t制表符，\n换行符
a = re.findall('\s', str4)
print('\s: ' + str(a))

str4 = '3.141592423'
# \S匹配非空字符串
a = re.findall('\S', str4)
print('\S:' + str(a))

# 修饰符re.I,不区分大小写
str5 = 'abcABCaBCABC'
a = re.findall('abc\w', str5, re.I)  # 不区分大小写
print(a)

# 修饰符 re.S 匹配所有字符
str5 = 'abc\ndef\tegfwf'
print(re.findall('.*', str5))
print(re.findall('.*', str5, re.S))

# ^匹配开头，$匹配结尾
list1 = ['abcde', 'deabc', 'ghabcdef']
print('^匹配开头，$匹配结尾:')
for i in list1:
    print(re.findall('^abc', i))
    print(re.findall('abc$', i))

```

