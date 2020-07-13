# 标签页切换

```python
from selenium import webdriver
import time

driver = webdriver.Chrome('/usr/local/bin/chromedriver')
driver.get('https://baidu.com')
driver.implicitly_wait(5)

# 点击百度热榜
element1 = driver.find_element_by_css_selector('.title-text').click()

# 获取当前打开的所有的标签页句柄 （唯一资源标识符）
all_handlers = driver.window_handles
for handler in all_handlers:
    driver.switch_to.window(handler)
    if driver.title == '百度搜索风云榜':
        # 点击小说页面
        element2 = driver.find_element_by_css_selector('#main-nav > li:nth-child(4) > a').click()
# print(all_handlers)
# driver.switch_to.window(all_handlers[1])

driver.close()

```

