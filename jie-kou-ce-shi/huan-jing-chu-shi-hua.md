# 环境初始化

### 定义

pytest 提供的fixture实现unittest中setup/teardown 功能，可以在每次执行case之前初始化数据。

### fixture 函数级别:

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

### Fixture 类级别:

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

