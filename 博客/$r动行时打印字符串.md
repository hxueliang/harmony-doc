**【问题】**

使用`$r()`引 string 资源时，打印的是`$r()`对象信息，期望打印的是`$()`引的字符串，如下图
![在这里插入图片描述](https://i-blog.csdnimg.cn/direct/166d3a750e8f4d0cba01a44685ff4113.png)

**【原因】**

`$r()`是编译时处理，不支持程序运行时动态改变

**【方案】**

运行时推荐使用`resourceManager`中的相关 api，如`getStringByName`

**【文档】**

https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-resource-manager-V5#getstringbyname9
