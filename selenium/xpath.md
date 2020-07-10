# XPath

```python
from selenium import webdriver

driver1 = webdriver.Chrome('/usr/local/bin/chromedriver')
driver1.get("https://m.weibo.cn/search?containerid=231583")

driver1.implicitly_wait(2)
# driver1.find_element_by_xpath('//*[@id="app"]/div[1]/div[1]/div[2]/div/div/div[8]/div/div/h4')

# 定位微博热搜榜
element1 = driver1.find_element_by_xpath('/html/body/div[1]/div[1]')
# 注意相对路径的点
result = element1.find_element_by_xpath('./div[1]/div[2]/div/div/div[8]/div/div/h4')
# 两个点则是上层目录
# result = element1.find_element_by_xpath('../div[1]/div[2]/div/div/div[8]/div/div/h4')

# / 一条斜杆是直接子元素
# // 两条斜杆则是从任意层级开始寻找

result.click()
```

