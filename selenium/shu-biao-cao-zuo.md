# 鼠标操作

```python
from selenium import webdriver
import time
from selenium.webdriver.common.action_chains import ActionChains

driver = webdriver.Chrome('/usr/local/bin/chromedriver')
driver.get('https://baidu.com')

# 定位到需要悬停的元素
element1 = driver.find_element_by_name('tj_briicon')
# 对定位到的元素执行鼠标悬停的操作
ActionChains(driver).move_to_element(element1).perform()

ActionChains(driver).context_click(element1).perform()
# 双击操作
ActionChains(driver).double_click(element1).perform()

# 拖动元素
driver.get('file:///Users/gabriel/PycharmProjects/trail1/selenium_note/mouse_test.html')
source = driver.find_element_by_id('blackSquare')
target = driver.find_element_by_id('targetEle')
ActionChains(driver).drag_and_drop(source, target).perform()
driver.close()

```

