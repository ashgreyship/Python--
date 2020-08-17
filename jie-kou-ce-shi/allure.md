# Allure

## 装饰器

![](../.gitbook/assets/image%20%2821%29.png)



@allure.feature ：用于定义被测试的功能，被测产品的需求点

@allure.story ： 用于定义被测功能的用户场景，即子功能点

@allure.step ：用于将一个测试用例，分成几个步骤在报告中输出

@allure.attach ： 用于向测试报告中输入一些附加的信息，通常是一些测试数据信息

### **设计用例级别**

**@allure.severity**

* blocker　 阻塞缺陷（功能未实现，无法下一步）
* critical　　严重缺陷（功能点缺失）
* normal　　 一般缺陷（边界情况，格式错误）
* minor　 次要缺陷（界面错误与ui需求不符）
* trivial　　 轻微缺陷（必须项无提示，或者提示不规范

environment.properties

