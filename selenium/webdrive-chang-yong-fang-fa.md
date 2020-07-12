# Webdrive常用方法

### 文本框清空

```python
from selenium import webdriver
import time

driver = webdriver.Chrome('/usr/local/bin/chromedriver')
driver.get('https://www.baidu.com')

element1 = driver.find_element_by_id('kw')
element1.send_keys('这是文本内容')
time.sleep(5)
# 文本框清空，和send_keys 一样，是针对input文本框进行操作
element1.clear()
time.sleep(5)

element1.send_keys('selenium')
element1.submit()
```

### 获取元素的属性值

```python
element1 = driver.find_element_by_id('su')
print(element1.get_attribute('value'))
```

### 检查标签是否可见

```python
element1 = driver.find_element_by_id('su')
print(element1.is_displayed())
```

### 返回元素的尺寸

```python
element1 = driver.find_element_by_id('su')
print(element1.size)
```

