## xpath 入门到进阶


#### 内容目录

1. XPath 简介
本章讲解 XPath 的概念。
2. XPath 节点
本章详细介绍 XPath 中不同类型的节点，以及节点之间的关系。
3. XPath 语法
本章讲解 XPath 的语法。
4. XPath 轴
本章讲解 XPath axes（轴）。
5. XPath 运算符
本章列出了可以用于 XPath 表达式的运算符。
6. XPath 实例
本章使用 "books.xml" 文档来演示一些 XPath 实例。
7. XPath 摘要
本文内容包括在本教程所学知识的一个总结，以及我们向你推荐的下一步应该学习的内容。
8. XPath 参考手册
9. XPath 函数
XPath 2.0、XQuery 1.0 和 XSLT 2.0 的内置函数。


Xpath:
- //标签                  表示从全局的子子孙孙中查找标签
- /标签                   表示从子代中查找标签
- 标签[@标签属性]           查找带有xxx属性的标签
- 标签[@标签属性="值"]      查找带有xxx属性=x值的标签
- 标签/@标签属性            查找标签xxx属性的值
- .//标签                 从当前标签中查找
- 
```
response = HtmlResponse(url='http://example.com', body=html,encoding='utf-8')
hxs = HtmlXPathSelector(response)
print(hxs)   # selector对象
hxs = Selector(response=response).xpath('//a')
print(hxs)    #查找所有的a标签
hxs = Selector(response=response).xpath('//a[2]')
print(hxs)    #查找某一个具体的a标签    取第三个a标签
hxs = Selector(response=response).xpath('//a[@id]')
print(hxs)    #查找所有含有id属性的a标签
hxs = Selector(response=response).xpath('//a[@id="i1"]')
print(hxs)    # 查找含有id=“i1”的a标签
hxs = Selector(response=response).xpath('//a[@href="link.html"][@id="i1"]')
print(hxs)   # 查找含有href=‘xxx’并且id=‘xxx’的a标签
hxs = Selector(response=response).xpath('//a[contains(@href, "link")]')
print(hxs)   # 查找 href属性值中包含有‘link’的a标签
hxs = Selector(response=response).xpath('//a[starts-with(@href, "link")]')
print(hxs)   # 查找 href属性值以‘link’开始的a标签
hxs = Selector(response=response).xpath('//a[re:test(@id, "i\d+")]')
print(hxs)   # 正则匹配的用法   匹配id属性的值为数字的a标签
hxs = Selector(response=response).xpath('//a[re:test(@id, "i\d+")]/text()').extract()
print(hxs)    # 匹配id属性的值为数字的a标签的文本内容
hxs = Selector(response=response).xpath('//a[re:test(@id, "i\d+")]/@href').extract()
print(hxs)    #匹配id属性的值为数字的a标签的href属性值
hxs = Selector(response=response).xpath('/html/body/ul/li/a/@href').extract()
print(hxs)    #抽取当前路径/html/body/ul/li/下a标签的href属性值
hxs = Selector(response=response).xpath('//body/ul/li/a/@href').extract_first()
print(hxs)    #抽取全局路径//body/ul/li/下a标签的href属性第一个值

备注：
xpath中支持正则的使用：    用法  标签[re:test（@属性值，"正则表达式"）]
获取标签的文本内容：   /text()     
获取第一个值：  selector_obj.extract_first()    
获取所有的值：  selector_obj.extract()  返回一个list
```