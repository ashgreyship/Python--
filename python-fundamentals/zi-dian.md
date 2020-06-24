# 字典

一种数据类型，它是通过键值对存储。

```python
dict1 = {'A':'Apple','B':'Book','C'：'Cake'}
```

键和值永远成对出现。

字典本身是无序的，不关注顺序。

值可以是任何类型的数据

在字典中，建必须是唯一的。

## 创建

如果不用字典：

```python
namelist = ['Mike',25,180,80],['Tom',26,178,82]
print(namelist[1][0])
```

使用字典：

```python
namelist2 = {'name':'Mike','age':'25','height':'170'
             ,'name':'Tom','age':'26','height':'180'}
```

当键为其他类型\(列表，元祖，字典\)：

```python
dict2 = {'abc':{'A':'B'}}
print(dict2)
```

## 增加

新增对象中的元素

如果字典中已经有这个键，则修改这个元素

如果字典中没有这个键，则新增这个元素

```python
dict2['AB'] = 'A2'
dict2.update({'AA':'CXK','AB':'YYQX'})
```

## 删除

删除键值对

```python
del dict['abc']
```

清空字典：

```python
dict2 = {}
dict2.clear()
print(dict2)
```

## 搜索

判断某个值是否在列表中，此处根据键来判断，并且区分大小写

```python
if 'AB' in dict2:
    print('在字典里')
```

## 读取

获取字典中所有的键，keys\(\) 方法的返回值属于**类列表**

```python
print(dict2.keys())
```

可以使用list\(\) 函数强制转换成真正的列表

```python
print(list(dict2.keys()))
```

获取字典中所有的值

```python
print(dicts.values())
```

## 遍历

同时获取值和键

```python
print(dict2.items())

for k,v in dict2.items():
    print((f'键:{k},值:{v}'))
```

## JSON 和字典

将json 转换为字典

```python
vipdata = ''' {
        "a" :"tom",
        "b":"alex"
}'''
tmp = json.loads(vipdata)
```

将字典转换为json

```python
json.dumps(temp)
```

从文件读取json

```python
with open('file-path') as ofile:
    tmp = json.load(ofile)
print(tmp)
    
```

json.loads 和 json.load 

在文件中读取json 数据，使用load方法。

将字典数据写入文件，用dump：

```python
with open ('file-path') as ifile:
    json.dump(tmp,ifile)
    ifile.seek(0)
    print(ifile.read())
```





