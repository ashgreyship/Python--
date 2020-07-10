# 断言

```python
from selenium import webdriver
import unittest

driver1 = webdriver.Chrome('/usr/local/bin/chromedriver')
driver1.get("https://baidu.com")

# class assert_test(unittest.TestCase):
#     def test_title(self):
#         # 获取当前页面的标题
#         self.assertEqual(driver1.title, '百度一下，你就知道')

assert driver1.title == '百度一下，你就知道'

# 获取当前页面的URL
print(driver1.current_url)
assert driver1.current_url == 'https://www.baidu.com/'

# 获取标签对之间的文本信息
element1 = driver1.find_element_by_css_selector(
    '#hotsearch-content-wrapper > li:nth-child(1) > a > span.title-content-title')
assert element1.text == '王振华不服判决上诉 法院受理'
driver1.close()

```

