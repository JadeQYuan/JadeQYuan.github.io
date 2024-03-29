title: XML
description: XML
categories: 
  - Java
  - 核心技术卷Ⅱ
author: Jade
date: 2022-01-15 16:00:00
---

{% markmap %}

## 2.1 XML概述
- 在许多情况下，想要描述的信息的结构比较复杂，属性文件（Property）不能很方便地处理它。
- 属性文件采用的使一种单一的平面层次结构。
- 属性文件要求键使唯一的。如果要存放一个值序列，则需要另一个变通方法。
- XML能够表示层次结构，并且重复的元素不会被曲解。
- XML和HTML都是古老的标准通用标记语言（Standard Generalized Markup Language， SGML）的衍生语言。

- XML是大小写敏感的。
- XML中结束标签不能省略。
- XML中属性值必须用引号括起来。
- XML中属性必须都有属性值。
- XML文档应当以一个文档头开始。文档头是可选的，但是强烈推荐使用文档头。
- 文档头之后是文档类型定义（Document Type Definition，DTD）。文档类型定义的是确保文档正确的一个重要机制，但它不是必需的。
- XML文档的正文包含根元素，根元素包含其他元素。
- 元素可以有子元素、文本或两者皆有。在设计XML文档结构时，应该避免混合式内容（【可以简化解析过程】）。
- 何时用元素，何时用属性。一个常用的经验法则是：属性只应该用来修改值的解释，而不是用来指定值。
- XML标记： 字符引用、实体引用、CDATA、处理指令、注释。

## 2.2 解析XML文档
- 要处理XML文档，就要先解析它。
- 解析器是这样一个程序：它读入一个文件，确认这个文件具有正确的格式，然后将其分解成各种元素，使得程序员能够访问这些元素。
- Java库提供了两种XML解析器：树型解析器、流机制解析器。
- 像文档对象模型（Document Object Model， DOM）解析器这样的树型解析器，它们将读入的XML文档转换成树结构。
- 像XML简单API（Simple API for XML， SAX）解析器这样的流机制解析器，它们在读入XML文档时生成响应的事件。
- DOM解析器的接口已经被W3C标准化了。org.w3c.dom包包含了这些接口类型的定义。
- 不同的提供者（比如Apache、IBM）都编写了实现这些接口的DOM解析器。Java XML处理API（JAXP）库使得实际上可以以插件形式使用这些解析器中的任意一个。
- JDK中也包含了自己的DOM解析器。
- Document、Element、Node。

## 2.3 验证XML文档
- XML解析器的一个很大的好处就是它能自动校验某个文档是否具有正确的结构。
- 如果要指定文档结构，可以提供一个文档类型定义或一个XML Schema定义。
- DTD或schema包含了用于解释文档应如何构成的规则，这些规则指定了每个元素的合法子元素和属性。
- 与DTD相比，XML Schema可以表达更加复杂的验证条件。与DTD语法不同，Schema使用XML，这为处理Schema文件带来了方便。
- XML Schema语言时设计用来替代DTD的。然而XML Schema很复杂，而且还远没有得到普遍的采纳。

- 提供DTD的方式有多种。1.纳入XML文档DOCTYPE声明中。2.存储在外面。SYSTEM声明。指定一个包含DTD的URL。3.来源于SGML的DTD机制。

- 如果要在文档中引用Schema文件，需要在根元素中添加属性。
- Schema使用命名空间定义了每个元素的类型。类型可以是简单类型，即有格式限制的字符串，或者是复杂类型。

## 2.4 使用XPath来定位信息
- XPath语言使得访问树节点变得很容易。
- XPath可以描述XML文档中的一个节点集。
- Java SE 5.0增加了一个API来计算XPath表达式。

## 2.5 使用命名空间
- Java语言使用包来避免名字冲突。XML也有类似的命名空间机制，可以用于元素名和属性名。
- 名字空间是由统一资源标识符（URI）来标识的。HTTP的URL格式是最常用的。
- 在命名空间的URL所表示的位置上不需要有任何文档，XML解析器不会尝试取该处查找任何东西。人们习惯于将解释该命名空间的文档放在URL位置上。
- HTTP URL作为命名空间的标识符容易确保它们是独一无二的。
- 命名空间本质上是嵌套的。
- 可以用一个前缀来表示命名空间，即为特定文档选取的一个短的表示符。Java中没有类似的机制。

## 2.6 流机制解析器
- 如果文档很大，并且处理算法又非常简单，可以在运行时解析节点，而不必看到完整的树形结构。 -- 流机制解析器。SAX、StAX。

- SAX解析器在解析XML输入的组成部分时会报告事件，但不会以任何方式存储文档，而是由事件处理器建立相应的数据结构。
- 实际上，DOM解析器是在SAX解析器的基础上建立起来的，它在接收到解析器事件使建立DOM树。
- 在使用SAX解析器时，需要一个处理器来为不同的解析器事件定义事件动作。ContentHandler接口定义了若干个在解析文档时解析器会调用的回调方法。

- StAX解析器是一种”拉解析器“，与安装事件处理器不同，只需使用基本循环来迭代所有的事件。

## 2.7 生成XML文档
- 不带命名空间的文档。
- 带命名空间的文档。
- 写出文档。XSLT。
- 使用StAX写XML文档。

## 2.8 XSL转换
- XSL转换（XSLT）机制可以指定将XML文档转换为其他格式的规则。
- XSLT通常用来将某种机器可读的XML格式转译为另一种机器可读的XML格式，或者将XML转译为适合人类阅读的表示格式。
- 需要提供XSLT样式表，它描述了XML文档向某种其他格式转换的规则。

{% endmarkmap %}
