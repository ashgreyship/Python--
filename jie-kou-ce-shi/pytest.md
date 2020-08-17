# PyTest

## 注意事项

.**py 测试文件**必须以`test_` 开头

**测试类**必须以Test开头，并且不能有init方法

**测试方法**必须以test\_开头

断言必须使用assert

## 数据驱动\(参数化\)

```python
pytest.mark.parametrize
```

第一个参数是字符串。第二个参数是列表，列表里嵌套元组。

## mark标签

对于Pytest, 我们可以在每一个模块，每一个类，每一个方法和用例前都加上marker, 那样我们在 pytest运行的时候就可以只运行带有该mark标签的模块，类，用例。

这样的话我们可以选择自动化时，可以选择执行全部用例，某个模块用例，某个流程用例，某个单独用例，总之就是某个单独的标签下的所有用例。

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

## conftest

倘若有多个.py 文件需要调用同一方法，将方法写入`conftest.py` 配置文件，`test_xxx.py` 测试文件中不需要 `import conftest`，pytest 会自动搜索同级目录中的 conftest.py 文件 

