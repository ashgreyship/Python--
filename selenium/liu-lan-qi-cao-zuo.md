# 浏览器操作

```python
from selenium import webdriver
import time

driver = webdriver.Chrome('/usr/local/bin/chromedriver')
driver.get('https://www.baidu.com')
driver.get('https://www.taobao.com')

# 浏览器后退
driver.back()
time.sleep(3)

# 浏览器前进
driver.forward()
time.sleep(3)

# 刷新界面
driver.refresh()

# 设置为全屏展示
driver.maximize_window()
time.sleep(3)

# 设置最小化
driver.minimize_window()

# 设置浏览器的高度和宽度，参数数字的大单位是像素点
driver.set_window_size(700, 700)

driver.close()
```

