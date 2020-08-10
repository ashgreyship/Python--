# 环境初始化

## 定义

`pytest` 提供的fixture实现`unittest`中setup/teardown 功能，可以在每次执行case之前初始化数据。

## Scope（作用域）

`function`（默认值）,

`class:` 每个类都会执行一次，类里面有多个方法调用，只在第一个方法执行时调用

`module:` 一个 .py文件执行一次

`package`

`session；`

## fixture 实例化顺序

* 高级别作用域的（例如：`session`）先于低级别的作用域的（例如：`class`或者`function`）实例化；
* 相同级别作用域的，其实例化顺序遵循它们在**测试用例中被声明的顺序（也就是形参的顺序）**，或者`fixture`之间的相互调用关系；
* 使能`autouse`的`fixture`，先于其同级别的其它`fixture`实例化；

## fixture 函数级别:

```python
#环境初始化

@pytest.fixture()  
def start1_func():
    print('---initialize---')


@pytest.fixture()
def start2_func():
    print('---initialize---')


def test_01(start1_func):
    print('---test01---')


def test_02(start2_func):
    print('---test02---')


def test_03(start1_func, start2_func):
    print('---test03---')
```

## Fixture 类级别:

```python
@pytest.fixture(scope='class')
def start1_func():
    print('---initialize---')


class Test00:  # 需要执行Test00这个测试类，需要做初始化

    def test_01(self, start1_func):
        print('---test01---')

    def test_02(self):
        print('---test02---')


if __name__ == '__main__':
    pytest.main(['test_fixture_demo.py', '-s'])
```

一个类中的所有方法都会使用环境初始化方法，整个类只执行一次初始化方法

## fixture 包级别：

此文件名字必须为 `conftest.py`

### 环境数据初始化

```python
import pytest

@pytest.fixture(scope='session', autouse=True)
def start_demo():
    print('整个包的初始化操作')
```

### 环境数据清除

```python
import pytest

@pytest.fixture(scope='session', autouse=True)
def start_demo(request):
    print('整个包的初始化操作')

    def fin():
        print('--测试完成，包的数据清除---')

    request.addfinalizer(fin)

```

## pytest.mark.usefixture\('fixture-name'\)

除了将fixture的方法作为参数传给某方法，也可以使用 `pytest.mark.usefixture`

此装饰器可以写在方法名字前面或者类前面

