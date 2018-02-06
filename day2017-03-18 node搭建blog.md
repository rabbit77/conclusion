## 搭建blog
1. app.set('port', process.env.PORT || 3001);  
在app.js文件里，端口号是这样配置的，但是服务器启动起来显示是3000，而且只要我把后边容错的写成3000，服务就没办法启动起来，提示3000端口被占。
2. app.get()和app.post() 是主要使用的http请求方式。
   app.get()和app.post() 第一个参数都是请求路径，第二个参数是处理请求的回调函数。回调函数里有两个参数，req和res，分别代表请求信息和响应信息。
   路径的请求及对应的获取路径有以下几种形式。
   req.query    处理get请求，获取get请求的参数
   req.params   处理 /:xxx形式的get或post请求，获取请求参数 ？？？？
   req.body     处理post请求，获取post请求参数
   req.param()  处理get和post请求，但查找优先级由高到低为req.params -> req.body -> req.query
3. ejs 中include包含文件，可以进行页面灵活布局
4. mongodb 命令行以 ./mongod 开头   
    可以使用 ./mongod --help 查看
            ./mongod --dbpath ../blog/ 设置blog文件夹作为工程的存储目录并启动数据库
