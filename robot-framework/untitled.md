# 基本语法

```python
# 配置表 导入第三方库
*** Settings ***
# 库名称 大小写敏感
Library   SeleniumLibrary


# 测试用例定义在表中---Test Case
# 表名称首字母大写---中间有空格
*** Test Cases ***
# 用例名称顶格来写，用例主体另起一行，并且有两个以上空格
testcase1

    # 关键词参数需要与关键词空两格以上
    log to console  执行用例1

search test
    [Documentation]  打开浏览器
    [Tags]  浏览器测试用例标签
    open browser   https://www.baidu.com/  chrome
    # 设置隐式等待
    set selenium implicit wait   10
    # 元素定位方式，值 或者元素定位方式=值
    input text  id=kw  松勤\n
    click element  id=su
    # 搜索结果页面校验
    ${actual}  get text  id=1
    log to console  ${actual}
    # 判断实际结果是否包括预期结果
    should contain  ${actual}     松勤网
    close browser
```

