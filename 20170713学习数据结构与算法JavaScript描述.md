1.   why so hard? I just wanna cry.
2.   看得有点困了😪，去看一会儿《JavaScript高级程序设计》

以下为记录🦂
1.  <script>标签定义了defer属性，脚本会被延迟到整个页面都解析完毕后再运行。相当于告诉浏览器先下载，但延迟执行。
2.  <script>标签的async属性立即下载，但不保证按照指定它们的先后顺序执行。异步加载页面其他内容。
3.  注释hack？
4.  标识符：指变量、函数、属性的名字，或者函数的参数。
5.  关键字可用于表示控制语句的开始或结束，或者用于执行特定操作等。
6.  如果定义的变量准备在将来用于保存对象，那么最好将该变量初始为null，这样只要检查null值就可以知道相应的变量是否已经保存了一个对象的引用。```if(car != null){}```
7.  任何对象转换为boolean值得时候都为true
8.  Object的每个实例都具有下列属性和方法。
    * constructor  保存着用于创建当前对象的函数。
    * hasOwnProperty(propertyName):用于检查给定的属性在当前对象实例中是否存在。
    * isPrototypeOf(object):用于检查传入的对象是否是传入对象的原型
    * propertyIsEnumerable(propertyName):用于检查给定的属性是否能够使用for-in语句来枚举。
    * toLocaleString():返回对象的字符串表示，该字符串与执行环境的地区对应。
    * toString():返回对象的字符串表示。
    * valueOf():返回对象的字符串、数值或布尔值表示。
9. 操作符：用于操作数据值的操作符，包括算数操作符、位操作符、关系操作符、相等操作符
10. 后置递增和递减操作是在包含它们的语句被求值之后才执行的。
11. 闭包是指有权访问另一个函数作用域中的变量的函数。
-----
## html5相关扩展
###  与类相关的扩充
1.  为了让开发人员适应并增加对class属性的新认识，html5新增了许多API，致力于简化css类的用法
*  getElementsByClassName()
*  classList 属性
    add(value)
    contains(value)
    remove(value)
    toggle(value)
###  焦点管理
辅助管理DOM焦点的功能
*  document.activeElement 始终会引用DOM中当前获得了焦点的元素。
*  document.hasFocus() 用于确定文档是否获得了焦点
###  HTMLDocument变化
*  document.readyState属性
    loading:正在加载文档；
    complete,已经加载完文档
* document.head 属性引用文档的<head>元素，作为对document.body引用文档的<body>元素的补充
###  字符集属性
charset
###  自定义数据属性
可以为元素添加非标准的属性，需要加前缀data-
###  插入标记
1. innerHTML 属性返回与调用元素的所有子节点
