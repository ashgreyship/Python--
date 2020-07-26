# 使用Weditor

[项目链接](https://github.com/alibaba/web-editor)

确保 ATX 可以安装在手机上

运行代码时候需要结束UIAUTOMATOR

原理类似 appium。也是在手机上安装代理程序（ATX）通过代理和本地服务通信，从而完成元素定位，截屏等功能。

{% hint style="danger" %}
若手机装不上ATX，可以尝试以下方法手动安装：
{% endhint %}

```python
pip install --pre --upgrade uiautomator2 #安装ui2
python -m uiautomator2 init #连上手机运行该命令
```



