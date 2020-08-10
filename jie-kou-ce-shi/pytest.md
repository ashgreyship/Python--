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



