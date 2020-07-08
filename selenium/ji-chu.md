# 基础

## 打开网页

```python
from selenium import webdriver

driver = webdriver.Chrome('/usr/local/bin/chromedriver')
driver.get("https://www.baidu.com")
driver.fullscreen_window()
#找到搜索框
input_element = driver.find_element_by_id('kw')
input_element.send_keys('百科')

#找到搜索按钮
search_element = driver.find_element_by_id('su')

search_element.click()

```

## 8中元素定位放手

```python
from selenium import webdriver

driver1 = webdriver.Chrome('/usr/local/bin/chromedriver')
driver1.get("https://www.google.com")

# 通过 id 属性定位,只返回匹配到的第一个元素
element1 = driver1.find_element_by_id('kw')
print(element1.text)

# 通过元素得到文本定位,只返回匹配到的第一个元素
element2 = driver1.find_element_by_name('')

# 通过xpath定位,只返回匹配到的第一个元素
element3 = driver1.find_element_by_xpath('/html/body/div/select/option[3]')
print(element3.text)

# 通过 css 表达式定位，只返回匹配到的第一个元素
element4 = driver1.find_element_by_css_selector(
    '#tsf > div:nth-child(2) > div.A8SBwf > div.FPdoLc.tfB0Bf > center > input.gNO89b')

# 根据链接文本定位（全匹配，不支持模糊定位），只返回匹配到的第一个元素
element5 = driver1.find_element_by_link_text("访问百度").click()

#根据链接文本定位（全匹配，支持模糊定位），只返回匹配到的第一个元素
element6 = driver1.find_element_by_partial_link_text("百度").click()

#根据标签定位，只返回匹配到的第一个元素
element7 = driver1.find_element_by_tag_name('span')

# 根据 class 属性定位
element8 = driver1.find_element_by_class_name('a2')


driver1.quit()

```
