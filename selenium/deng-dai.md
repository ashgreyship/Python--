# 显示等待&隐式等待

代码加载过快，元素未加载成功，代码已经跑到这个元素了，所以会出现无法定位到元素的情况。因此需要设置等待时间。

## Sleep:

```python
from selenium import webdriver
import unittest
import time

driver1 = webdriver.Chrome('/usr/local/bin/chromedriver')
driver1.get("https://m.weibo.cn")

element1 = driver1.find_element_by_css_selector(
    '#app > div.main-wrap > div.lite-topbar.main-top > div.nav-top > a > aside > label > div')
element1.click()

time.sleep(1)
element1 = driver1.find_element_by_css_selector(
    '#app > div:nth-child(1) > div:nth-child(1) > div.card.m-panel.card16.m-col-2 > div > div > div:nth-child(8) > '
    'div > div > h4')
element1.click()

time.sleep(1)
element1 = driver1.find_element_by_css_selector(
    '#app > div:nth-child(1) > div:nth-child(1) > div:nth-child(2) > div > div > div:nth-child(1) > div > div > div > '
    'div > span.main-link.m-box.m-box-center-a > span.main-text.m-text-cut')
element1.click()

```

## 隐式等待\(Implicit Waits\)

它的作用范围就是Webdriver对象实例的整个生命周期。

```python
from selenium import webdriver

# 执行到某个元素的时候，先去看元素是否能被定位。
# 能则继续执行，
# 不能则稍微等一下，以轮询的方式等待，每隔一段时间检查一次，直到元素出现
# 有一个最大时间，超过最大时间还没有出现，则报错

driver1 = webdriver.Chrome('/usr/local/bin/chromedriver')
driver1.get("https://m.weibo.cn")

element1 = driver1.find_element_by_css_selector(
    '#app > div.main-wrap > div.lite-topbar.main-top > div.nav-top > a > aside > label > div')
element1.click()

# 设置隐式等待，只对之后的元素定位有效
# 默认参数为秒
# 如下代码设置的最大等待时间为20秒
# 当脚本执行到某个元素定位的时候，能定位则继续执行，
# 否则，以轮询的方式不断判断元素是否能被定位到
driver1.implicitly_wait(20)
element1 = driver1.find_element_by_css_selector(
    '#app > div:nth-child(1) > div:nth-child(1) > div.card.m-panel.card16.m-col-2 > div > div > div:nth-child(8) > '
    'div > div > h4')
element1.click()

driver1.implicitly_wait(20)
element1 = driver1.find_element_by_css_selector(
    '#app > div:nth-child(1) > div:nth-child(1) > div:nth-child(2) > div > div > div:nth-child(1) > div > div > div > '
    'div > span.main-link.m-box.m-box-center-a > span.main-text.m-text-cut')
element1.click()

driver1.close()
```

## 显示等待\(Explicit Waits\)

```python
from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions

# 执行到某个元素的时候，先去看元素是否能被定位。
# 能则继续执行，
# 不能则稍微等一下，以轮询的方式等待，每隔一段时间检查一次，直到元素出现
# 有一个最大时间，超过最大时间还没有出现，则报错
from selenium.webdriver.support.wait import WebDriverWait

driver1 = webdriver.Chrome('/usr/local/bin/chromedriver')
driver1.get("https://m.weibo.cn")

element1 = driver1.find_element_by_css_selector(
    '#app > div.main-wrap > div.lite-topbar.main-top > div.nav-top > a > aside > label > div')
element1.click()

# 每隔0.5 秒 检查一次，最多等待十秒
element2 = WebDriverWait(driver1, 10, 0.5).until(
    expected_conditions.visibility_of_element_located(
        (By.CSS_SELECTOR,
         '#app > div:nth-child(1) > div:nth-child(1) > div.card.m-panel.card16.m-col-2 > div > div > div:nth-child(8) '
         '> div > div > h4'))
)

element2.click()

driver1.close()

```

## 隐式等待&显示等待

* 显示等待要等到满足某个元素的某个条件,该条件满足后就往下执行代码，如果超出设置的时间还没满足条件,那么就抛出Exception。
* 显式等待使用ExpectedConditions类中的方法， 可以设置显试等待的条件



* 隐式等待对之后所有元素等待都生效
* 它的作用范围就是Webdriver对象实例的整个生命周期。

