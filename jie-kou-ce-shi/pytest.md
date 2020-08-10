# PyTest

## 注意事项

.py 测试文件必须以`test_` 开头

测试类必须以Test开头，并且不能有init方法

测试方法必须以test\_开头

断言必须使用assert

## 标签

![](../.gitbook/assets/image%20%2815%29.png)

### 创建标签

```python
@pytest.mark.<name>
```

创建 `pytest.ini` 文件。

```python
[pytest]
markers =
    lesson: teach_lesson
    lesson_add: lesson_add
    lesson_list: teach_lesson_list
```

### 使用标签

![](../.gitbook/assets/image%20%2817%29.png)

```python
pytest.main(['test_lessson.py','-s','-m','mark_name1'])

'-m','not mark_name1'
'-m','mark_name1 or mark_name2'
```

![](../.gitbook/assets/image%20%2814%29.png)

### -k 和 -v:

```python
-k <name > 
#匹配用例名称
#匹配: 可全名，也可以模糊

#加入现在有两个文件: lesson_1.py lesson_2.py 
pytest -k lesson

-v <节点>
#比如 test_lesson.py::TestLesson::test_lesson_add
pytest -v test_lesson.py::TestLesson::test_lesson_add

-sq: 简化 print 打印信息
-s 输出打印
- 

```

### 跳过/条件跳过

* 跳过-- skip
* 有条件的跳过-skipif

```python
@pytest.mark.skip("跳过原因")
@pytest.mark.skipif(1==2,reason='原因')
```

