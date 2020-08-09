# 环境初始化

环境初始化与清除

pytest 提供的fixture实现unittest中setup/teardown 功能，可以在每次执行case之前初始化数据。

### fixture 基本用法:

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



