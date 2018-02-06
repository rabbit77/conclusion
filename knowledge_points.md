##  al
1.  项目中用到了哪些技术？项目如何进行依赖管理？描述项目的结构（前端工程化）？
* 优信新车前期使用requirejs进行依赖管理，后期重构之后用webpack打包进行依赖管理
   这里简单解释一下AMD。
    异步模块规范API定义了一种模块机制，这种机制下，模块和它的依赖可以异步加载。这个非常适合于浏览器环境，因为同步的加载模块会对性能、可用性、debug调试、跨域访问产生问题。
    AMD在浏览器环境下有着自己的独特优势：
        由于源码和浏览器加载的一致，所见即所得，代码编写和debug非常方便。尤其是在多页面的web项目下，不同页面的脚本js是根据依赖关系异步按需加载的，不用手动处理每个页面加载js脚本的情况。
    但是AMD引用第三方库的时候比较麻烦，如果第三方库不支持AMD，必须手动配置，重用性会比较差
    ---
    commonjs in browser
    由于CommonJS的require是同步的，在require处需要阻塞，这个在浏览器上并没有很好的支持（浏览器只能异步加载脚本，并没有同步的文件I/0），CommonJS在浏览器上直接使用必须有一个build的过程，在这个build的过程里进行依赖关系的解析与做好映射。这里有一个典型的实现就是substack的browserify。
    browserify可以像nodejs一样使用require(),browserify会递归的解析依赖关系，并把这些依赖全部build成一个bundle文件，在浏览器使用一个<script>标签引入即可

    webpack 是一个模块打包工具，

    ---
    web前端工程化
    就是把一整套前端工作流程中能用工具搞定的部分，用工具搞定。
    比如，以前创建配置初始项目文件结构和文件，以前靠复制，现在输入命令自动完成；
    以前校验JS文件是否规范，你可能复制放到jslint上检验，现在配置grunt监听文件变动自动校验显示校验结果；
    现在修改代码有一大堆插件可以监听文件变动，自动刷新；
    以前压缩合并文件用手工复制到压缩工具然后复制到一个文件里，现在配置grunt等自动监听文件变动，自动合并压缩。
    以前发布到服务器上，要手动使用FTP软件上传，现在也可以用工具自动打包上传。

    node服务：用于实现前后端分离，核心功能是实现数据代理中转，附带url路由分发及服务端渲染功能
    web应用开发


2.  


##  mt
1.  BFC(block formatting context)
    是web页面的可视化CSS渲染的一部分，它是块盒子的布局发生，浮动互相交互的区域。
    一个块格式化上下文由以下之一创建：
    *  根元素或其它包含它的元素
    *  浮动（元素的float不是none）
    *  绝对定位的元素（元素具有position为absolute或fixed）
    *  内联块（元素具有display:inline-block）
    *  表格单元格（元素具有display:table-cell）
    *  表格标题（元素具有display:table-caption）
    *  块元素具有overflow,且值不是visible

一个块格式化上下文包括创建它的元素内部所有内容，除了被包含于创建新的块级格式化上下文的后代元素内的元素。
定位和清除浮动的样式规则只适用于处于同一格式化上下文内的元素。浮动不会影响其他块格式化上下文中元素的布局，并且清除浮动只能清除同一块格式化上下文中在它前面的元素的浮动。

2. call、apply、bind的区别
    *  call和apply都是为了改变某个函数运行时的上下文而存在的（就是为了改调用变函数内部this的指向）；
    *  apply的第二个参数是一个数组，call的第二个及其以后的参数都是数组里边的元素，就是说都要列举出来；
    *  用法：验证是否是数组
        ```
        function isArray(obj){
            return Object.prototype.toString.call(obj)==='[Object Array]'
        }
        ```
    *  让类数组拥有数组的方法
        ```
        Array.prototype.slice.apply(argument);
        ```
        或者
        ```
        [].slice.apply(argument);
        ```
    *  bind 也是改变函数体内this指向；
    *  bind会创建一个新函数，称为绑定函数，调用这个函数时，绑定函数会以创建它时传入bind()方法的第一个参数作为this，传入bind()方法的第二个及以后的参数加上绑定函数运行时本身的参数按照顺序作为原函数的参数来调用原函数；
    *  bind与call和apply最大的区别是，bind不会立即调用，而其他会立即调用。

3.  实现bind的底层代码
    ```
        if(!Function.prototype.bind){
            Function.prototype.bind = function(oThis){
                if(typeof this !== 'function'){
                    throw new TypeError('Function.prototype.bind-what is trying to bound is not callable');
                }
                var args = [].slice.call(arguments,1),//获取bind函数从第二个参数到最后一个参数
                fToBind = this,
                fNOP = function(){},
                fBound = function(){
                    return fToBind.apply(this instanceof fNOP ? this : oThis , args.concat([].slice.call(arguments)))
                }
                if(this.prototype){
                    fNOP.prototype = this.prototype
                }
                fBound.prototype = new fNOP()
                return fBound;
            };
        }
    ```
    [].slice.call(arguments, 1)返回的是arguments数组从1号位开始的片段。
    bind函数的两个特点：返回一个函数，可以传入一个参数
    一个绑定函数也能使用new操作符创建对象，提供的this值被忽略，同时调用时的参数被提供给模拟函数。
    也就是说当bind返回的函数作为构造函数的时候，bind时指定的this值会失效，但是传入的参数依然生效
4.  多维数组转一维
    * 方法一 map()
    ```
    var arr = [1,2,[3,4],5,5];
    function uid(arr){
        var arr1 = (arr+'').split(',');//将数组转换成字符串，然后用,分隔成一个一个的数组
        var arr2 = arr1.map(x=>Number(x));
        return arr2;
    }
    ```
    * 方法二 递归
    ```
    var arr = [1,2,[3,4],5,5];
    var newArr = [];
    function fun(arr){
        for(var i = 0 ; i<arr.length;i++){
            if(Array.isArray(arr[i])){
                fun(arr[i])
            }else{
                newArr.push(arr[i])
            }
        }

    }
    fun(arr);

    ```
5. react虚拟dom怎么实现的
    虚拟dom是在dom的基础上建立了一个抽象层，我们对数据和状态所做的任何改动，都会自动且高效的同步到虚拟dom，最后再批量同步到dom中。
    react会在内存中维护一个虚拟dom树，当我们对这个树进行读或者写的时候，实际上是对虚拟dom进行的，当数据变化时，react会自动更新虚拟dom，然后拿新的虚拟dom与旧的虚拟dom进行对比，找到有变更的部分，得出一个patch，然后将这些patch放到一个队列里，最终批量更新这些patch到dom中。
