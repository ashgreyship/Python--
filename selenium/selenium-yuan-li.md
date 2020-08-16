# Selenium 原理



1. 对于每一条Selenium脚本，一个http请求会被创建并且发送给浏览器的驱动
2. 浏览器驱动中包含了一个HTTP Server，用来接收这些http请求
3. HTTP Server接收到请求后根据请求来具体操控对应的浏览器
4. 浏览器执行具体的测试步骤
5. 浏览器将步骤执行结果返回给HTTP Server
6. HTTP Server又将结果返回给Selenium的脚本，如果是错误的http代码我们就会在控制台看到对应的报错信息。

**那为什么同一个浏览器驱动即可以处理Java语言的脚本，也可以处理Python语言的脚本呢？**

这就要提到WebDriver基于的协议：**JSON Wire protocol**。

关于WebDriver的协议也是面试的时候经常会问到的问题。

JSON Wire protocol是在http协议基础上，对http请求及响应的body部分的数据的进一步规范。

我们知道在HTTP请求及响应中常常包括以下几个部分：http请求方法、http请求及响应内容body、http响应状态码等。

