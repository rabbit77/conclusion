###   express API
1.  jsonp 的定义？

    JSONP是JSON with padding(填充式JSON或参数式JSON)的简写，是应用JSON的一种新方法，在后来的web应用中非常流行。
    JSONP看起来与JSON差不多，只不过是被包含在函数调用中的JSON，eg
    callback({"name":"mei"})

    JSONP由两部分构成，回调函数及数据。回调函数是当响应到来时应该在页面中调用的函数。回调函数的名字一般在请求中指定。
    而数据传入的就是回调函数中的JSON数据。
2.  app.engine(ext, callback)
    注册模板引擎的 callback 用来处理ext扩展名的文件 默认情况下, 根据文件扩展名require() 对应的模板引擎。
    比如你想渲染一个 "foo.jade" 文件，Express会在内部执行下面的代码，然后会缓存require()，这样就可以提高后面操作的性能。
    app.engine('jade',require('jade')._ _ express);
    在车伯乐项目中使用ejs模板渲染.html文件，写法为
    app.engine('.html',require('ejs')._ _ express);
    app.set('view engine', 'html')

    不过这里为什么注册了模板引擎，还要set view engine 呢？设置view engine的值为html？
3. res.redirect([status],url)
    [status]状态码 默认为302 Found    
    url  跳转到相应页面的路径

    请求服务器的状态码归纳------->

    1xx  信息
    100  Continue   服务器仅接收到部分请求，但是一旦服务器并没有拒绝该请求，客户端应该继续发送其余的请求
    101  Switching Protocols  服务器转换协议：服务器将遵从客户的请求转换到另外一种协议

    2xx  成功
    200  OK   请求成功（其后是对GET和POST请求的应答文档）
    201  Created  请求被创建完成，同时新的资源被创建
    202  Accepted 供处理的请求已被接受，但是处理未完成
    203  Non-authoritative Information  文档已经正常的返回，但一些应答头可能不正确，因为使用的是文档的拷贝
    204  No Content  没有新文档。浏览器应该继续显示原来的文档。如果用户定期地刷新页面，而Servlet可以确定用户文档足够新，这个状态代码是很有用的
    205  Reset Content  没有新文档。但浏览器应该重置它所显示的内容。用来强制浏览器清除表单输入内容。
    206  Partial Content  客户发送了一个带有Range头的GET请求，服务器完成了它。

    3xx  重定向
    300  Multiple Choices  多重选择。链接列表。用户可以选择某链接到达目的地，最多可以选择5个地址
    301  Moved Permanently  所请求的页面已转移至新的url（永久重定向）
    302  Found  所请求的页面已经临时转移至新的url
    303  See Other  所请求的页面可在别的url下被找到
    (表示状态码也太多了吧，改天再写~~~懒人就是这样炼成的)

4. 图像ping解决跨域
    可以动态创建图像，使用它们的onload和onerror事件处理程序来确定是否接收到了响应。
    所以遇到javascript模板写的标签，行内绑定onerror事件报错的时候，是不是可以去js里边调用img.onerror方法？

5. 加鹏给我发过来汽车之家做的全景VR的链接，让我研究研究，但是表示无从下手啊~

6.
