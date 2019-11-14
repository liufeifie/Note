# NPM
## 基本操作
*npm不需要单独安装。在安装Node的时候，会连带一起安装npm*

### 版本
```
npm –v  // 查看当前NPM的版本
```

### 升级
*不过由于nodejs更新速度要慢于 npm ，因此在一般情况下要升级npm到最新版本*
```
npm install npm -g
```

### 帮助
```
npm help // npm命令或npm help命令查看帮助引导说明
npm help <command> // 可以查看具体的命令说明
npm -l // 查看各个命令的简单用法
```

### 安装依赖包

#### 本地安装
```
npm install express
```

#### 全局安装
> 全局模式并不是将一个模块包安装为一个全局包的意思，它并不意味着可以从任何地方通过require()来引用到它，它的主要目的是命令行工具的使用
```
npm install express -g
npm root -g // 查看全局安装目录
```

#### 其他安装
> 对于一些没有发布到NPM上的包，或是因为网络原因导致无法直接安装的包，可以通过将包下载到本地，然后以本地安装。本地安装只需为NPM指明package.json文件所在的位置即可：它可以是一个包含package.json的存档文件，也可以是一个URL地址，也可以是一个目录下有package.json文件的目录位置。具体参数如下：
```
npm install <tarball file>
npm install <tarball url>    
npm install <folder>
```

#### 镜像安装
在执行命令时，添加--registry=http://registry.url ，示例如下：
```
npm install underscore --registry=http://registry.url
或
npm install underscore  registry "http://registry.npm.taobao.org"

npm config delete registry // 取消镜像
```

**错误**
```
npm err! registry error parsing json
镜像的问题，取消镜像即可

ResponseError: Hostname/IP doesn't match certificate's altnames
淘宝镜像需要使用http，而不是https

ResponseError: Hostname/IP doesn't match certificate's altnames:
　　更改为如下镜像即可
npm install underscore  registry "http://registry.npm.taobao.org"
```

#### 版本
```
npm install express // 默认安装最新
npm install express@3.9.0 // 安装指定版本 使用@标志符
npm install // 项目依赖的包都在package.json文件里声明
```

#### 参数
##### 参数-S
--save表示安装包信息将加入到dependencies（生产阶段的依赖）
```
npm install express --save 或 npm install express -S

package.json 文件的 dependencies 字段：
"dependencies": {
    "express": "^3.9.0"
}
```
##### 参数-D
--save-dev表示安装包信息将加入到devDependencies（开发阶段的依赖），所以开发阶段一般使用它
```
npm install express --save-dev 或 npm install express -D

package.json 文件的 devDependencies字段：
"devDependencies": {
    "express": "^3.9.0"
}
```

#### 镜像安装
```　
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

#### 查看及修改
```
npm ls // 查看安装了哪些包
npm ls -g // 查看全局安装了哪些包
npm ls <pkgname> // 查看特定依赖包的信息（安装目录和版本）
npm info <pkgname>  // 查看更详细信息
npm outdated <pkgname> // 检查模块是否过时
npm update <pkgname> // 更新模块（win10不可更新）
npm install <pkgname> // 可以更新
npm uninstall <pkgname> // 解析卸载模块
```

#### 发布依赖包
##### 编写模块
模块的内容随意编写
```
exports.sayHello = function () {
    return 'Hello, world.'
}
```
##### 初始化包描述文件
```
npm init 
```
##### 注册包仓库账号
npm 的帐号，密码和邮箱
```
npm adduser
```
##### 上传包
```
npm publish <folder> // npm publish .  所有文件
```
##### 安装包
```
npm install <包名>
```
##### 错误总结：
1. 此包名已经被注册
[![](https://upload-images.jianshu.io/upload_images/7262870-3d181d9b6cbd8011.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)]( "")
2. 邮箱未验证
[![](https://upload-images.jianshu.io/upload_images/7262870-3d002f38881a68c9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)]( "")
3. 镜像问题
[![](https://upload-images.jianshu.io/upload_images/7262870-eda68ef117c18b48.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1000/format/webp)]( "")

执行：npm config set registry=http://registry.npmjs.org

##### npm撤销（24小时内可以撤销）
```
npm unpublish <包名> --force
```

npm config set registry http://registry.cnpmjs.org/



# PATH
> const path = require('path')  可用来访问这个模块

## 路径组成
### path.dirname(p)
> 返回路径p所在的目录
```
path.dirname('C:/Users/Desktop/github/study/node/index.js') // C:/Users/Desktop/github/study/node

path.dirname('C:/test/aaa')  // C:/test
```

### path.basename(p[, ext])
> 返回路径的最后一个部分，即文件名。参数ext为需要截掉的后缀内容　
```
path.basename('C:/Users/Desktop/github/study/node/index.js') // index.js
path.basename('C:/Users/Desktop/github/study/node/index.js', 'js') // index
```

### path.extname(p)
> 返回路径p的扩展名，从最后一个'.'到字符串的末尾。如果最后一个部分没有'.'，或者路径是以'.'开头，则返回空字符串
```
path.extname('/foo/bar/baz/asdf/a.txt') // .txt
path.extname('/foo/bar/baz/asdf/a.txt.b') // .b
path.extname('/foo/bar/baz/asdf/a.')  // .
path.extname('C:/test/aaa/.') // ''
path.extname('C:/test/aaa')  // ''
```

## 分隔符
### path.sep
> 返回对应平台下的文件分隔符，win下为'\'，*nix下为'/'
```
path.sep  // win下为\，*nix下为/
```

### path.delimiter
> 返回对应平台下的路径分隔符，win下为';'，*nix下为':'
```
path.delimiter //win下为“;”，*nix下为“:”
```

## 规范化
### path.normalize(p)
> 规范化路径，处理冗余的“..”、“.”、“/”字符。发现多个斜杠时，会替换成一个斜杠。当路径末尾包含一个斜杠时，保留。Windows系统使用反斜杠

### path.join([path1], [path2], [...])
> 将多个路径结合在一起，并转换为规范化路径　

## 绝对和相对
### path.resolve([from ...], to)
> 从源地址 from 到目的地址 to 的绝对路径，类似在shell里执行一系列的cd命令

### path.isAbsolute(path)
> path是一个绝对路径(比如 'E:/abc')，或者是以“/”开头的路径，二者都会返回true

### path.relative(from, to)
> 获取从 from 到 to 的相对路径，可以看作 path.resolve 的相反实现


# Express
## 安装
```
$ mkdir myapp // 创建工作目录
$ cd myapp // 进入工作目录
$ npm init // 为应用创建一个 package.json 文件
$ npm install express --save // 安装 Express 并将其保存到依赖列表中
```

## 服务器
```
// routes/index.js
module.exports = function (app) {
  app.get('/', function (req, res) {
    res.send('Hello world');
  });
  app.get('/customer', function(req, res){
    res.send('customer page');
  });
  app.get('/admin', function(req, res){
    res.send('admin page');
  });
};
// index.js
const express = require('express');
const app = express();
const routes = require('./routes')(app);
app.listen(8080);
```

## 生成器
> 通过应用生成器工具 express 可以快速创建一个应用的骨架
```
// 安装工具
npm install express-generator -g
// 生成工作目录
express myapp
// 安装所有依赖包
cd myapp
npm install

//启动
DEBUG=myapp npm start // MacOS 或 Linux 平台
set DEBUG=myapp & npm start // win 平台
```

# HTTP
> Express框架建立在node.js内置的http模块上。http模块生成服务器的原始代码如下
```
const http = require("http");

const app = http.createServer(function(request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello world!");
});

app.listen(8080, "localhost");
```

>上面代码的关键是http模块的createServer方法，表示生成一个HTTP服务器实例。该方法接受一个回调函数，该回调函数的参数，分别为代表HTTP请求和HTTP回应的request对象和response对象。

*Express框架的核心是对http模块的再包装。上面的代码用Express改写如下*
```
const express = require('express')
const app = express()
app.get('/', function(req, res){
  res.send('Hello World')
})
app.listen(8080)
```
*比较两段代码，可以看到它们非常接近。原来是用http.createServer方法新建一个app实例，现在则是用Express的构造方法，生成一个Epress实例。两者的回调函数都是相同的。Express框架等于在http模块之上，加了一个中间层*

# 中间件
## 概述
> Express 是一个自身功能极简，完全是由路由和中间件构成一个的 web 开发框架：从本质上来说，一个 Express 应用就是在调用各种中间件

>简单说，中间件（middleware）就是处理HTTP请求的函数。它最大的特点就是，一个中间件处理完，再传递给下一个中间件。App实例在运行过程中，会调用一系列的中间件

>每个中间件可以从App实例，接收三个参数，依次为request对象（代表HTTP请求）、response对象（代表HTTP回应），next回调函数（代表下一个中间件）。每个中间件都可以对HTTP请求（request对象）进行加工，并且决定是否调用next方法，将request对象再传给下一个中间件

>中间件的功能包括：1、执行任何代码；2、修改请求和响应对象；3、终结请求-响应循环；4、调用堆栈中的下一个中间件

>如果当前中间件没有终结请求-响应循环，则必须调用 next() 方法将控制权交给下一个中间件，否则请求就会挂起

## 分类
> Express 应用可使用如下几种中间件：  
1、应用级中间件；2、路由级中间件；3、错误处理中间件；4、内置中间件；5、第三方中间件

1. 应用级中间件绑定到 app 对象 使用 app.use() 和 app.METHOD()，其中， METHOD 是需要处理的 HTTP 请求的方法，例如 GET, PUT, POST 等等，全部小写
2. 路由级中间件绑定的对象为 express.Router()
3. 错误处理中间件和其他中间件定义类似，只是要使用 4 个参数，而不是 3 个，其签名如下： (err, req, res, next)
```
// 不进行任何操作、只传递request对象的中间件:
app.use(function(req, res, next) {
  next()
});

// next就是下一个中间件。如果它带有参数，则代表抛出一个错误，参数为错误文本:
app.use(function(req, res, next) {
  next('404')
});

// 错误处理中间件:
app.use(function(err, req, res, next) {
  console.error(err.stack)
  res.status(500).send('Something broke!')
});

```
4. express.static 是 Express 唯一内置的中间件。它基于 serve-static，负责在 Express 应用中提托管静态资源
5. 通过使用第三方中间件从而为 Express 应用增加更多功能。安装所需功能的 node 模块，并在应用中加载，可以在应用级加载，也可以在路由级加载。下面的例子安装并加载了一个解析 cookie 的中间件： cookie-parser
```
$ npm install cookie-parser
const express = require('express');
const app = express();
const cookieParser = require('cookie-parser');

// 加载用于解析 cookie 的中间件
app.use(cookieParser());
```

## use方法
use是express注册中间件的方法，它返回一个函数。下面是一个连续调用两个中间件的例子
```
var express = require("express");
var http = require("http");

var app = express();

app.use(function(request, response, next) {
  console.log("In comes a " + request.method + " to " + request.url);
  next();
});

app.use(function(request, response) {
  response.writeHead(200, { "Content-Type": "text/plain" });
  response.end("Hello world!\n");
});

http.createServer(app).listen(1337);
```
*上面代码使用app.use方法，注册了两个中间件。收到HTTP请求后，先调用第一个中间件，在控制台输出一行信息，然后通过next方法，将执行权传给第二个中间件，输出HTTP回应。由于第二个中间件没有调用next方法，所以request对象就不再向后传递了。*

use方法内部可以对访问路径进行判断，据此实现简单的路由，根据不同的请求网址，返回不同的网页内容
```
var express = require("express");
var http = require("http");

var app = express();

app.use(function(request, response, next) {
  if (request.url == "/") {
    response.writeHead(200, { "Content-Type": "text/plain" });
    response.end("Welcome to the homepage!\n");
  } else {
    next();
  }
});

app.use(function(request, response, next) {
  if (request.url == "/about") {
    response.writeHead(200, { "Content-Type": "text/plain" });
  } else {
    next();
  }
});

app.use(function(request, response) {
  response.writeHead(404, { "Content-Type": "text/plain" });
  response.end("404 error!\n");
});

http.createServer(app).listen(1337);
```

上面代码通过request.url属性，判断请求的网址，从而返回不同的内容。注意，app.use方法一共登记了三个中间件，只要请求路径匹配，就不会将执行权交给下一个中间件。因此，最后一个中间件会返回404错误，即前面的中间件都没匹配请求路径，找不到所要请求的资源。

　　除了在回调函数内部判断请求的网址，use方法也允许将请求网址写在第一个参数。这代表，只有请求路径匹配这个参数，后面的中间件才会生效。无疑，这样写更加清晰和方便
```
app.use('/path', someMiddleware);
```
　　上面代码表示，只对根目录的请求，调用某个中间件。

因此，上面的代码可以写成下面的样子
```
var express = require("express");
var http = require("http");

var app = express();

app.use("/home", function(request, response, next) {
  response.writeHead(200, { "Content-Type": "text/plain" });
  response.end("Welcome to the homepage!\n");
});

app.use("/about", function(request, response, next) {
  response.writeHead(200, { "Content-Type": "text/plain" });
  response.end("Welcome to the about page!\n");
});

app.use(function(request, response) {
  response.writeHead(404, { "Content-Type": "text/plain" });
  response.end("404 error!\n");
});

http.createServer(app).listen(1337);
```

# 托管静态资源
>  express.static 是 Express 唯一内置的中间件，负责在 Express 应用中提托管静态资源，例如图片、CSS、JavaScript 文件等
express.static(root, [options])

　　参数 root 指提供静态资源的根目录，可选的 options 参数拥有如下属性
```
属性        　　类型    　 缺省值 　　　　描述
dotfiles    　　String   “ignore” 　　是否对外输出文件名以点开头的文件。可选值为allow、deny和ignore
etag        　　Boolean   true 　　　　是否启用 etag 生成
extensions  　　Array    [] 　　　　　　设置文件扩展名备份选项
index        　 Mixed    “index.html” 发送目录索引文件，设置为 false 禁用目录索引。
lastModified    Boolean  true 　设置Last-Modified头为文件在操作系统上的最后修改日期。可选值为true或false
maxAge          Number   0 　　　　　　以毫秒或者其字符串格式设置 Cache-Control 头的 max-age 属性。
redirect        Boolean  true 　　　　当路径为目录时，重定向至 “/”。
setHeaders      Function      　　　　设置 HTTP 头以提供文件的函数。


var options = {
  etag: false,
  extensions: ['htm', 'html'],
  index: false,
  maxAge: '1d',
  redirect: false,
  setHeaders: function (res, path, stat) {
    res.set('x-timestamp', Date.now());
  }
}
app.use(express.static(__dirname + '/public', options));

app.use(express.static('public'));

// 静态资源存放在多个目录下面，可以多次调用 express.static 中间件
app.use(express.static('public'));
app.use(express.static('files'));

// 如果希望所有通过 express.static 访问的文件都存放在一个“虚拟（virtual）”目录（即目录根本不存在）下面，可以通过为静态资源目录指定一个挂载路径的方式来实现，如下所示：

app.use('/static', express.static('public'));
```
# 常用中间件
## cookie-parser()
用于解析cookie的中间件，添加中间后，req具备cookies属性。通过req.cookies.xxx可以访问cookie的值
```
$ npm install cookie-parser
```

### app.use(cookieParser(secret, options))
> secret 是可选参数，用于对cookie进行签名 ，通过它可以判断出客户是否修改了cookie，这是处于安全考虑，这个参数是任意字符串

> options 可选参数，是一个json对象，可选项包括path、expires、maxAge、domain、secure、httpOnly

```
var express = require('express')
var cookieParser = require('cookie-parser')
 
var app = express()
app.use(cookieParser())
 
app.get('/', function(req, res) {
  console.log('Cookies: ', req.cookies)
})
 
app.listen(8080)
```

## express-session
>session运行在服务器端，当客户端第一次访问服务器时，可以将客户的登录信息保存。 当客户访问其他页面时，可以判断客户的登录状态，做出提示，相当于登录拦截。session可以和Redis或者数据库等结合做持久化操作，当服务器挂掉时也不会导致某些客户信息（购物车）丢失。

　　当浏览器访问服务器并发送第一次请求时，服务器端会创建一个session对象，生成一个类似于key,value的键值对， 然后将key(cookie)返回到浏览器(客户)端，浏览器下次再访问时，携带key(cookie)，找到对应的session(value)。客户的信息都保存在session中
```
$ npm install express-session
```

### app.use(session(options))
> options 常用选项如下：  
　　name - 默认'connect.sid'，可自定义  
　　store - session 储存器实例  
　　secret - 用于对cookie进行签名 ，通过它可以判断出客户是否修改了cookie，这是处于安全考虑，这个参数是任意字符串  
　　cookie - 对session cookie的设置 。默认值 { path: '/', httpOnly: true, secure: false, maxAge: null }  
　　genid -  是个函数，调用它来生成一个新的会话ID。 （默认：使用UID2库）  
　　rolling -  强制对每个响应的Cookie，重置到期日期。 （默认：false）  
　　resave - 每一次都重新保存，即使没修改过（默认：true）  
　　proxy - ture／false，是否支持trust proxy,，需要设置 app.enable('trust proxy');一般来说，无需设置  
　　常用方法如下：  
　　Session.destroy() :删除session，当检测到客户端关闭时调用  
　　Session.reload() :当session有修改时，刷新session  
　　Session.regenerate() ：将已有session初始化  
　　Session.save() ：保存session  
```
var express = require('express');
var cookieParser = require('cookie-parser');
var session = require('express-session');
 
app.use(cookieParser('sessiontest'));
app.use(session({
 secret: 'sessiontest', //与cookieParser 中的一致
 resave: true,
 saveUninitialized:true
}));

//修改router/index.js,第一次请求时保存一条用户信息。
router.get('/', function(req, res, next) {
 var user={
  name:"Chen-xy",
  age:"22",
  address:"bj"
 }
 req.session.user=user;
 res.render('index', {
  title: 'the test for nodejs session' ,
  name:'sessiontest'
 });
});


//修改router/users.js，判断用户是否登陆。
router.get('/', function(req, res, next) {
 if(req.session.user){
  var user=req.session.user;
  var name=user.name;
  res.send('你好'+name+'，欢迎来到我的家园。');
 }else{
  res.send('你还没有登录，先登录下再试试！');
 }
});
```

## serve-favicon
> 设置网站的 favicon图标
```
npm install serve-favicon

var express = require('express')
var favicon = require('serve-favicon')
var path = require('path')
 
var app = express()
app.use(favicon(path.join(__dirname, 'public', 'favicon.ico')))
 
// Add your routes here, etc. 
 
app.listen(3000)
```

## body-parser
> bodyParser用于解析客户端请求的body中的内容，内部使用JSON编码处理，url编码处理以及对于文件的上传处理
```
npm install body-parser
```
1. 底层中间件用法：这将拦截和解析所有的请求；这种用法是全局的。
```
var express = require('express')
var bodyParser = require('body-parser')
  
var app = express()
  
// parse application/x-www-form-urlencoded
app.use(bodyParser.urlencoded({ extended: false }))
// extended:boolean是urlencoded的参数，如果是true可以解析nested的json格式，如果是false的话则不可以
  
// parse application/json
app.use(bodyParser.json())
  
app.use(function (req, res) {
 res.setHeader('Content-Type', 'text/plain')
 res.write('you posted:\n')
 res.end(JSON.stringify(req.body, null, 2))
})
```
use方法调用body-parser实例；且use方法没有设置路由路径；这样的body-parser实例就会对该app所有的请求进行拦截和解析

2. 特定路由下的中间件用法：这种用法是针对特定路由下的特定请求的，只有请求该路由时，中间件才会拦截和解析该请求；也即这种用法是局部的；也是最常用的一个方式
```
var express = require('express')
var bodyParser = require('body-parser')
  
var app = express()
  
// create application/json parser
var jsonParser = bodyParser.json()
  
// create application/x-www-form-urlencoded parser
var urlencodedParser = bodyParser.urlencoded({ extended: false })
  
// POST /login gets urlencoded bodies
app.post('/login', urlencodedParser, function (req, res) {
 if (!req.body) return res.sendStatus(400)
 res.send('welcome, ' + req.body.username)
})
  
// POST /api/users gets JSON bodies
app.post('/api/users', jsonParser, function (req, res) {
 if (!req.body) return res.sendStatus(400)
 // create user in req.body
})
```
express的post（或者get）方法调用body-parser实例；且该方法有设置路由路径；这样的body-parser实例就会对该post（或者get）的请求进行拦截和解析

3. 设置Content-Type 属性；用于修改和设定中间件解析的body内容类型
```
// parse various different custom JSON types as JSON
app.use(bodyParser.json({ type: 'application/*+json' });
 
// parse some custom thing into a Buffer
app.use(bodyParser.raw({ type: 'application/vnd.custom-type' }));
 
// parse an HTML body into a string
app.use(bodyParser.text({ type: 'text/html' }));
```

## morgan
> Mogran是一个node.js关于http请求的express默认的日志中间件
```
npm install  morgan

// basic.js
var express = require('express');
var app = express();
var morgan = require('morgan');

app.use(morgan('short'));
app.use(function(req, res, next){
    res.send('ok');
});

app.listen(3000);
```
node basic.js运行程序，并在浏览器里访问 http://127.0.0.1:3000 ，打印日志如下
```
::1 - GET / HTTP/1.1 200 2 - 3.157 ms
::1 - GET / HTTP/1.1 304 - - 0.784 ms
```

#### morgan支持stream配置项，可以通过它来实现将日志落地的效果，代码如下：
```
var express = require('express');
var app = express();
var morgan = require('morgan');
var fs = require('fs');
var path = require('path');

var accessLogStream = fs.createWriteStream(path.join(__dirname, 'access.log'), {flags: 'a'});

app.use(morgan('short', {stream: accessLogStream}));
app.use(function(req, res, next){
    res.send('ok');
});

app.listen(3000);
```
> morgan的API非常少，使用频率最高的就是morgan()，作用是返回一个express日志中间件

> morgan(format, options)
　　参数说明如下：  
　　format：可选，morgan与定义了几种日志格式，每种格式都有对应的名称，比如combined、short等，默认是default  
　　options：可选，配置项，包含stream（常用）、skip、immediate  
　　stream：日志的输出流配置，默认是process.stdout  
　　skip：是否跳过日志记录  
　　immediate：布尔值，默认是false。当为true时，一收到请求，就记录日志；如果为false，则在请求返回后，再记录日志  

# 路由
## 路由方法
> 针对不同的请求，Express提供了use方法的一些别名，这些别名是和 HTTP 请求对应的路由方法： get、post、put、head、delete、options、trace、copy、lock、mkcol、move、purge、propfind、proppatch、unlock、report、mkactivity、checkout、merge、m-search、notify、subscribe、unsubscribe、patch、search 和 connect

> app.all() 是一个特殊的路由方法，没有任何 HTTP 方法与其对应，它的作用是对于一个路径上的所有请求加载中间件

>有些路由方法名不是合规的 JavaScript 变量名，此时使用括号记法，比如 app['m-search']('/', function ...
```
var express = require("express");
var http = require("http");
var app = express();

app.all("*", function(request, response, next) {
  response.writeHead(200, { "Content-Type": "text/plain" });
  next();
});

app.get("/", function(request, response) {
  response.end("Welcome to the homepage!");
});

app.get("/about", function(request, response) {
  response.end("Welcome to the about page!");
});

app.get("*", function(request, response) {
  response.end("404!");
});

http.createServer(app).listen(1337);
```
上面代码的all方法表示，所有请求都必须通过该中间件，参数中的“*”表示对所有路径有效。get方法则是只有GET动词的HTTP请求通过该中间件，它的第一个参数是请求的路径。由于get方法的回调函数没有调用next方法，所以只要有一个中间件被调用了，后面的中间件就不会再被调用了

## 路由路径
> 路由方法的第一个参数，都是请求的路径，称为路由路径，它可以是字符串、字符串模式或者正则表达式
```
　　1、字符串匹配
// 匹配 /about 路径的请求
app.get('/about', function (req, res) {
  res.send('about');
});

　　2、字符串模式匹配
// 匹配 acd 和 abcd
app.get('/ab?cd', function(req, res) {
  res.send('ab?cd');
});

　　3、正则表达式匹配
// 匹配任何路径中含有 a 的路径：
app.get(/a/, function(req, res) {
  res.send('/a/');
});
```

## 路由句柄
>　可以为请求处理提供多个回调函数，其行为类似中间件。唯一的区别是这些回调函数可能调用 next('route') 方法而略过其他路由回调函数。可以利用该机制为路由定义前提条件，如果在现有路径上继续执行没有意义，则可将控制权交给剩下的路径

*路由句柄有多种形式，可以是一个函数、一个函数数组，或者是两者混合*
1. 使用一个回调函数处理路由
```
app.get('/a', function (req, res) {
  res.send('Hello World!');
});
```
2. 使用多个回调函数处理路由
```
app.get('/b', function (req, res, next) {
  console.log('response will be sent by the next function ...');
  next();
}, function (req, res) {
  res.send('Hello World!');
});
```
3. 使用回调函数数组处理路由
```
var cb0 = function (req, res, next) {
  console.log('CB0');
  next();
}
var cb1 = function (req, res, next) {
  console.log('CB1');
  next();
}
var cb2 = function (req, res) {
  res.send('Hello World!');
}
app.get('/c', [cb0, cb1, cb2]);
```
4. 混合使用函数和函数数组处理路由
```
var cb0 = function (req, res, next) {
  console.log('CB0');
  next();
}
var cb1 = function (req, res, next) {
  console.log('CB1');
  next();
}
app.get('/d', [cb0, cb1], function (req, res, next) {
  console.log('response will be sent by the next function ...');
  next();
}, function (req, res) {
  res.send('Hello World!');
});
```

## 链式路由句柄
> 可使用 app.route() 创建路由路径的链式路由句柄。由于路径在一个地方指定，这样做有助于创建模块化的路由，而且减少了代码冗余和拼写错误
```
app.route('/e')
  .get(function(req, res) {
    res.send('Get a random c');
  })
  .post(function(req, res) {
    res.send('Add a c');
  })
  .put(function(req, res) {
    res.send('Update the c');
  });
```

# 路由器实例
> 从Express 4.0开始，路由器功能成了一个单独的组件Express.Router。它好像小型的express应用程序一样，有自己的use、get、param和route方法  
　　可使用 express.Router 类创建模块化、可挂载的路由句柄。Router 实例是一个完整的中间件和路由系统，因此常称其为一个 “mini-app”

## 基本用法
> 首先，Express.Router是一个构造函数，调用后返回一个路由器实例。然后，使用该实例的HTTP动词方法，为不同的访问路径，指定回调函数；最后，挂载到某个路径
```
var express = require('express');
var router = express.Router();
router.get('/', function(req, res) {
  res.send('首页');
});
router.get('/about', function(req, res) {
  res.send('关于');
});
app.use('/', router);
```
*上面代码先定义了两个访问路径，然后将它们挂载到根目录。如果最后一行改为app.use(‘/app’, router)，则相当于为/app和/app/about这两个路径，指定了回调函数。*

## router.route方法
> router实例对象的route方法，可以接受访问路径作为参数
```
var express = require('express');
var router = express.Router();
router.route('/api')
    .post(function(req, res) {
        // ...
    })
    .get(function(req, res) {
        res.send('api');
    });
app.use('/', router);
```

## router中间件
> use方法为router对象指定中间件，在数据正式发给用户之前，对数据进行处理。
```
router.use(function(req, res, next) {
    console.log(req.method, req.url);
    next();    
});
```

## 对路径参数的处理
>router对象的param方法用于路径参数的处理
```
router.param('name', function(req, res, next, name) {
    // 对name进行验证或其他处理……
    console.log(name);
    req.name = name;
    next();    
});
router.get('/hello/:name', function(req, res) {
    res.send('hello ' + req.name + '!');
});
```
上面代码中，get方法为访问路径指定了name参数，param方法则是对name参数进行处理
*[注意]param方法必须放在HTTP动词方法之前*

## 实例
```
// birds.js
var express = require('express');
var router = express.Router();

// 该路由使用的中间件
router.use(function timeLog(req, res, next) {
  console.log('Time: ', Date.now());
  next();
});
// 定义网站主页的路由
router.get('/', function(req, res) {
  res.send('Birds home page');
});
// 定义 about 页面的路由
router.get('/about', function(req, res) {
  res.send('About birds');
});

module.exports = router;

// app.js
var birds = require('./birds');
...
app.use('/birds', birds);
```
*应用即可处理发自 /birds 和 /birds/about 的请求，并且调用为该路由指定的 timeLog 中间件*

# 响应方法
> response对象包含以下9个方法，response对象的方法向客户端返回响应，终结请求响应的循环。如果在路由句柄中一个方法也不调用，来自客户端的请求会一直挂起  
```
方法    　　　　　　　描述  
res.download()     提示下载文件。  
res.end()     　　 终结响应处理流程。  
res.json()    　　 发送一个 JSON 格式的响应。  
res.jsonp()    　　发送一个支持 JSONP 的 JSON 格式的响应。  
res.redirect()     重定向请求。  
res.render()    　 渲染视图模板。  
res.send()    　　 发送各种类型的响应。  
res.sendFile()     以八位字节流的形式发送文件。  
res.sendStatus()   设置响应状态代码，并将其以字符串形式作为响应体的一部分发送。  
```

## 1、response.download方法
```
//下载路径为'/report-12345.pdf'的文件
res.download('/report-12345.pdf');

//下载路径为'/report-12345.pdf'的文件，并将文件命名为 'report.pdf'
res.download('/report-12345.pdf', 'report.pdf');

//下载路径为'/report-12345.pdf'的文件，将文件命名为 'report.pdf'，并且回调
res.download('/report-12345.pdf', 'report.pdf', function(err){
  if (err) {
    console.error(err)
  } else {
    console.error('下载成功')
  }
});
```

## 2、response.end方法

```
//终结响应处理流程
res.end();
//设置响应码为404，并终结响应处理流程
res.status(404).end();
```

## 3、response.json方法
```
res.json(null)
res.json({ user: 'tobi' })
res.status(500).json({ error: 'message' })
```

## 4、response.jsonp方法
```
res.jsonp(null)
res.jsonp({ user: 'tobi' })
res.status(500).jsonp({ error: 'message' })
```

## 5、response.redirect方法
```
res.redirect('/foo/bar');
res.redirect('http://example.com');
res.redirect(301, 'http://example.com');
res.redirect('../login');
```

## 6、response.render方法
```
res.render('index');
res.render('index', function(err, html) {
  res.send(html);
});
res.render('user', { name: 'Tobi' }, function(err, html) {
  // ...
});
```

## 7、response.send方法
```
res.send(new Buffer('whoop'));
res.send({ some: 'json' });
res.send('<p>some html</p>');
res.status(404).send('Sorry, we cannot find that!');
res.status(500).send({ error: 'something blew up' });
```

## 8、response.sendFile方法
```
response.sendFile("/path/to/anime.mp4");
```

## 9、response.sendStatus方法
```
res.sendStatus(200); // 'OK'
res.sendStatus(403); // 'Forbidden'
res.sendStatus(404); // 'Not Found'
res.sendStatus(500); // 'Internal Server Error'
```

# 请求方法

## req.params
```
// GET /user/tj
req.params.name
// => "tj"

// GET /file/javascripts/jquery.js
req.params[0]
// => "javascripts/jquery.js"
```

## req.query
```
// GET /search?q=tobi+ferret
req.query.q
// => "tobi ferret"

// GET /shoes?order=desc&shoe[color]=blue&shoe[type]=converse
req.query.order
// => "desc"

req.query.shoe.color
// => "blue"

req.query.shoe.type
// => "converse"
```

## req.body

```
// POST user[name]=tobi&user[email]=tobi@learnboost.com
req.body.user.name
// => "tobi"

req.body.user.email
// => "tobi@learnboost.com"

// POST { "name": "tobi" }
req.body.name
// => "tobi"
```

## req.param(name)
```
// ?name=tobi
req.param('name')
// => "tobi"

// POST name=tobi
req.param('name')
// => "tobi"

// /user/tobi for /user/:name 
req.param('name')
// => "tobi"
```

## req.cookies
```
// Cookie: name=tj
req.cookies.name
// => "tj"
```

## req.ip
```
req.ip
// => "127.0.0.1"
## req.path

// example.com/users?sort=desc
req.path
// => "/users"
## req.host

// Host: "example.com:3000"
req.host
// => "example.com"
```

# app方法
## set方法
> set方法用于指定变量的值
```
app.set("views", __dirname + "/views");
app.set("view engine", "jade");
```
*上面代码使用set方法，为系统变量“views”和“view engine”指定值*

## get方法
> 除了作为use()方法的别名用法外，get方法还用于获取变量的值，与set方法相对应
```
app.get('title');
// => undefined

app.set('title', 'My Site');
app.get('title');
// => "My Site"
```

## app.enable(name)
> 将设置项 name 的值设为 true 
```
app.enable('trust proxy');
app.get('trust proxy');
// => true
```

## app.disable(name)
> 将设置项 name 的值设为 false 
```
app.disable('trust proxy');
app.get('trust proxy');
// => false
```

## app.enabled(name)
> 检查设置项 name 是否已启用
```
app.enabled('trust proxy');
// => false

app.enable('trust proxy');
app.enabled('trust proxy');
// => true
```

## app.disabled(name)
> 检查设置项 name 是否已禁用
```
app.disabled('trust proxy');
// => true

app.enable('trust proxy');
app.disabled('trust proxy');
// => false
```

## app.engine(ext, callback)
> 注册模板引擎的 callback 用来处理 ext 扩展名的文件

*默认情况下, 根据文件扩展名 require() 加载相应的模板引擎。 比如想渲染一个 “foo.jade” 文件，Express 会在内部执行下面的代码，然后会缓存 require() ，这样就可以提高后面操作的性能*
```
app.engine('jade', require('jade').__express);
```

*那些没有提供 .__express 的或者想渲染一个文件的扩展名与模板引擎默认的不一致的时候，也可以用这个方法。比如想用EJS模板引擎来处理 “.html” 后缀的文件:*
```
app.engine('html', require('ejs').renderFile);
```

*有些模板引擎没有遵循这种转换， 这里有一个小项目 consolidate.js专门把所有的node流行的模板引擎进行了包装，这样它们在 Express 内部看起来就一样了。*
```
var engines = require('consolidate');
app.engine('haml', engines.haml);
app.engine('html', engines.hogan);
```

## app.locals
> 应用程序本地变量会附加给所有的在这个应用程序内渲染的模板。
```
app.locals.title = 'My App';
app.locals.strftime = require('strftime');
```
*app.locals 对象是一个 JavaScript Function，执行的时候它会把属性合并到它自身，提供了一种简单展示已有对象作为本地变量的方法。*
```
app.locals({
  title: 'My App',
  phone: '1-250-858-9990',
  email: 'me@myapp.com'
});

app.locals.title
// => 'My App'

app.locals.email
// => 'me@myapp.com'
```

app.locals 对象最终会是一个 Javascript 函数对象，不可以使用 Functions 和 Objects 内置的属性，比如 name、apply、bind、call、arguments、length、constructor。
```
app.locals({name: 'My App'});

app.locals.name
// => 返回 'app.locals' 而不是 'My App' (app.locals 是一个函数 !)
// => 如果 name 变量用在一个模板里，则返回一个 ReferenceError 
```

默认情况下Express只有一个应用程序级本地变量，它是 settings
```
app.set('title', 'My App');
// 在 view 里使用 settings.title
```

## app.render(view, [options], callback)
> 渲染 view ， 回调函数 callback 用来处理返回的渲染后的字符串。这个是 res.render() 的应用程序级版本，它们的行为是一样的。
```
app.render('email', function(err, html){
    // ...
});

app.render('email', { name: 'Tobi' }, function(err, html){
    // ...
});
```

## app.listen()
> 在给定的主机和端口上监听请求，这个和 node 文档中的 http.Server#listen() 是一致的。
```
var express = require('express');
var app = express();
app.listen(3000);
```
express() 返回的 app 实际上是一个 JavaScript Function，它被设计为传给 node 的 http servers 作为处理请求的回调函数。因为 app 不是从 HTTP 或者 HTTPS 继承来的，它只是一个简单的回调函数，可以以同一份代码同时处理 HTTP 和 HTTPS 版本的服务。
```
var express = require('express');
var https = require('https');
var http = require('http');
var app = express();

http.createServer(app).listen(80);
https.createServer(options, app).listen(443);
```
app.listen() 方法只是一个快捷方法，如果想使用 HTTPS ，或者同时提供 HTTP 和 HTTPS ，可以使用上面的代码。
```
app.listen = function(){
  var server = http.createServer(this);
  return server.listen.apply(server, arguments);
};
```

# HTTPS
> 使用Express搭建HTTPS加密服务器
```
var fs = require('fs');
var options = {
  key: fs.readFileSync('E:/ssl/myserver.key'),
  cert: fs.readFileSync('E:/ssl/myserver.crt'),
  passphrase: '1234'
};

var https = require('https');
var express = require('express');
var app = express();

app.get('/', function(req, res){
  res.send('Hello World Expressjs');
});

var server = https.createServer(options, app);
server.listen(8084);
console.log('Server is running on port 8084');
```

# 模板引擎
> 需要在应用中进行如下设置才能让 Express 渲染模板文件： 

views, 放模板文件的目录，比如： 
```
app.set('views', './views')  
```
　　view engine, 模板引擎，比如：
``` 
app.set('view engine', 'jade')
```
## 设置html为模板引擎
view engine修改为ejs，并将模板的后缀修改为.html
```
npm install ejs
var ejs = require('ejs');
// 指定模板文件的后缀名为html
app.set('view engine', 'html');
//运行ejs引擎读取html文件
app.engine('.html', ejs.__express);

```

然后安装相应的模板引擎 npm 软件包
```
$ npm install jade --save
```
在 views 目录下生成名为 index.jade 的 Jade 模板文件，内容如下：
```
html
  head
    title!= title
  body
    h1!= message
```
　　然后创建一个路由渲染 index.jade 文件。如果没有设置 view engine，需要指明视图文件的后缀，否则就会遗漏它
```
app.get('/', function (req, res) {
  res.render('index', { title: 'Hey', message: 'Hello there!'});
});
```
此时向主页发送请求，“index.jade” 会被渲染为 HTML

# 数据库
>为 Express 应用添加连接数据库的能力，只需要加载相应数据库的 Node.js 驱动即可。这里简要介绍如何为 Express 应用添加和使用一些常用的数据库 Node 模块

## mysql
```
$ npm install mysql

var mysql  = require('mysql');
var connection = mysql.createConnection({
  host: 'localhost',
  user: 'dbuser',
  password: 's3kreee7'
});

connection.connect();

connection.query('SELECT 1 + 1 AS solution', function(err, rows, fields) {
  if (err) throw err;
  console.log('The solution is: ', rows[0].solution);
});

connection.end();
```

# 开发实例


















# express框架(request,response方法汇总)

```
Response 对象 - response 对象表示 HTTP 响应，即在接收到请求时向客户端发送的 HTTP 响应数据。常见属性有：

res.app：同req.app一样
res.append()：追加指定HTTP头
res.set()在res.append()后将重置之前设置的头
res.cookie(name，value [，option])：设置Cookie
opition: domain / expires / httpOnly / maxAge / path / secure / signed
res.clearCookie()：清除Cookie
res.download()：传送指定路径的文件
res.get()：返回指定的HTTP头
res.json()：传送JSON响应
res.jsonp()：传送JSONP响应
res.location()：只设置响应的Location HTTP头，不设置状态码或者close response
res.redirect()：设置响应的Location HTTP头，并且设置状态码302
res.send()：传送HTTP响应
res.sendFile(path [，options] [，fn])：传送指定路径的文件 -会自动根据文件extension设定Content-Type
res.set()：设置HTTP头，传入object可以一次设置多个头
res.status()：设置HTTP状态码
res.type()：设置Content-Type的MIME类型


Request 对象 - request 对象表示 HTTP 请求，包含了请求查询字符串，参数，内容，HTTP 头部等属性。常见属性有：

req.app：当callback为外部文件时，用req.app访问express的实例
req.baseUrl：获取路由当前安装的URL路径
req.body / req.cookies：获得「请求主体」/ Cookies
req.fresh / req.stale：判断请求是否还「新鲜」
req.hostname / req.ip：获取主机名和IP地址
req.originalUrl：获取原始请求URL
req.params：获取路由的parameters
req.path：获取请求路径
req.protocol：获取协议类型
req.query：获取URL的查询参数串
req.route：获取当前匹配的路由
req.subdomains：获取子域名
req.accepts()：检查可接受的请求的文档类型
req.acceptsCharsets / req.acceptsEncodings / req.acceptsLanguages：返回指定字符集的第一个可接受字符编码
req.get()：获取指定的HTTP请求头
req.is()：判断请求头Content-Type的MIME类型
```


# PROCESS 进程
> process对象是一个全局对象，在任何地方都能访问到它

## 概述
process是一个全局对象，即global对象的属性，可以在任何地方直接访问到它而无需引入额外模块
```
console.log(process === global.process);//true
console.log(process);
```

## 属性
### process.argv
> 包含命令行参数的数组。第一个元素会是'node'，第二个元素将是.js文件的名称，接下来的参数依次是命令行参数
```
process.argv  : 
    [ 'D:\\node\\node.exe',
      'C:\\Users\\Administrator\\Desktop\\github\\study\\node\\index.js' ]
```

### process.execArgv
> 启动进程所需的 node 命令行参数。这些参数不会在 process.argv 里出现，并且不包含 node 执行文件的名字，或者任何在名字之后的参数。这些用来生成子进程，使之拥有和父进程有相同的参数

### process.execPath
> 开启当前进程的执行文件的绝对路径
```
process.execPath  :  D:\node\node.exe
```

### process.env
> 获取当前系统环境信息的对象，常规可以用来进一步获取环境变量、用户名等系统信息

### process.version
> 一个暴露编译时存储版本信息的内置变量NODE_VERSION的属性
```
process.version : v10.14.2
```

### process.versions
> 一个暴露存储node以及其依赖包版本信息的属性

### process.pid
> 当前进程的 PID

### process.arch
> 返回当前CPU的架构('arm'、'ia32' 或者 'x64')

### process.platform
> 运行程序所在的平台系统 'darwin', 'freebsd', 'linux', 'sunos' or 'win32'

## 方法
### process.cwd
> 返回当前进程的工作目录
```
process.cwd  :  C:\Users\Administrator\Desktop\github\study\node
```

### process.chdir(directory)
> 改变当前工作进程的目录，如果操作失败抛出异常

### process.memoryUsage()
> 返回一个对象，它描述了Node进程的内存使用情况，其单位是bytes

### process.uptime()
>返回 Node 程序已运行的秒数

### process.hrtime()
> 返回当前的高分辨时间，形式为 [秒，纳秒] 的元组数组

*它是相对于在过去的任意时间。该值与日期无关，因此不受时钟漂移的影响。主要用途是可以通过精确的时间间隔，来衡量程序的性能*

### process.kill(pid, [signal])
> 结束对应某pid的进程并发送一个信号（若没定义信号值则默认为'SIGTERM'）

```
process.kill(process.pid, 'SIGTERM') 
```
  
### process.abort()
> 触发node的abort事件，退出当前进程

### process.exit([code])
> 终止当前进程并返回给定的code。如果省略了code，退出时会默认返回成功的状态码('success' code) 也就是0

### process.exitCode
> 可以自定义退出进程时node shell捕获到的状态码（必须是正常结束进程或者使用process.exit()指令退出）

*[注意]如果指明了 process.exit(code) 中退出的错误码 (code)，则会覆盖掉 process.exitCode 的设置*
```
process.exitCode = 4;
process.exit();//[Finished in 0.2s with exit code 4]
```

## 输入输出流
### process.stdout
> 一个指向标准输出流(stdout)的可写的流(Writable Stream)
```
process.stdout.write('这是一行数据\n这是第二行数据');
```

### process.stdin
> 一个指向标准输入流(stdin)的可读流(Readable Stream)。标准输入流默认是暂停(pause)的，所以必须要调用process.stdin.resume()来恢复(resume)接收
```
process.stdin.resume();
var a, b;
process.stdout.write('请输入a的值: ');
process.stdin.on('data', function (data) {
  if (a == undefined) {
    a = Number(data);
    process.stdout.write('请输入b的值: ');
  } else {
    b = Number(data);
    process.stdout.write('结果是: ' + (a + b));
    process.exit();
  }
})
```

## 事件
### 事件'exit'
> 当进程将要退出时触发
```
process.on('exit', function () {
  // 设置一个延迟执行
  setTimeout(function () {
    console.log('主事件循环已停止，所以不会执行');
  }, 0);
  console.log('退出前执行');
});
setTimeout(function () {
  console.log('运行到最后');
}, 500);
```

### 事件'uncaughtException'
> 捕获那些没有try catch的异常错误
```
//捕获到一个异常
process.on('uncaughtException', function(error) {
    console.log('捕获到一个异常', error);
});
var a = '123';
a.a(); //触发异常事件
console.log('这句话不会显示出来');
```

### 事件'SIGINT'
> 捕获当前进程接收到的信号（如按下了 ctrl + c）
```
process.on('SIGINT', function () {
  console.log('收到 SIGINT 信号。');
});
console.log('试着按下 ctrl + C');
setTimeout(function () {
  console.log('end');
}, 15000);
```

## nextTick
### process.nextTick(callback)
> 该方法算是 process 对象最重要的一个属性方法了，表示在事件循环（EventLoop）的下一次循环中调用 callback 回调函数。这不是 setTimeout(fn, 0) 函数的一个简单别名，因为它的效率高多了。该函数能在任何 I/O 事前之前调用回调函数。如果想要在对象创建之后而I/O操作发生之前执行某些操作，那么这个函数就十分重要了

>　　Node.js是单线程的，除了系统IO之外，在它的事件轮询过程中，同一时间只会处理一个事件。可以把事件轮询想象成一个大的队列，在每个时间点上，系统只会处理一个事件。即使电脑有多个CPU核心，也无法同时并行的处理多个事件。但也就是这种特性使得node.js适合处理I／O型的应用。在每个I／O型的应用中，只需要给每一个输入输出定义一个回调函数即可，他们会自动加入到事件轮询的处理队列里。当I／O操作完成后，这个回调函数会被触发。然后系统会继续处理其他的请求

>　　在这种处理模式下，process.nextTick()的意思就是定义出一个动作，并且让这个动作在下一个事件轮询的时间点上执行
```
function compute() {
  // performs complicated calculations continuously
  process.nextTick(compute);
}
http.createServer(function (req, res) {
  res.writeHead(200, { 'Content-Type': 'text/plain' });
  res.end('Hello World');
}).listen(5000, '127.0.0.1');
compute();
```

在这种模式下，我们不需要递归的调用compute()，只需要在事件循环中使用process.nextTick()定义compute()在下一个时间点执行即可。在这个过程中，如果有新的http请求进来，事件循环机制会先处理新的请求，然后再调用compute()。反之，如果把compute()放在一个递归调用里，那系统就会一直阻塞在compute()里，无法处理新的http请求了

　　当然，我们无法通过process.nextTick()来获得多CPU下并行执行的真正好处，这只是模拟同一个应用在CPU上分段执行而已

##【总结】

　　Nodejs的特点是事件驱动，异步I/O产生的高并发，产生此特点的引擎是事件循环，事件被分门别类地归到对应的事件观察者上，比如idle观察者，定时器观察者，I/O观察者等等，事件循环每次循环称为Tick，每次Tick按照先后顺序从事件观察者中取出事件进行处理

　　调用setTimeout()或setInterval()时创建的计时器会被放入定时器观察者内部的红黑树中，每次Tick时，会从该红黑树中检查定时器是否超过定时时间，超过的话，就立即执行对应的回调函数。setTimeout()和setInterval()都是当定时器使用，他们的区别在于后者是重复触发，而且由于时间设的过短会造成前一次触发后的处理刚完成后一次就紧接着触发

　　由于定时器是超时触发，这会导致触发精确度降低，比如用setTimeout设定的超时时间是5秒，当事件循环在第4秒循到了一个任务，它的执行时间3秒的话，那么setTimeout的回调函数就会过期2秒执行，这就是造成精度降低的原因。并且由于采用红黑树和迭代的方式保存定时器和判断触发，较为浪费性能

　　使用process.nextTick()所设置的所有回调函数都会放置在数组中，会在下一次Tick时所有的都立即被执行，该操作较为轻量，时间精度高

　　setImmediate()设置的回调函数也是在下一次Tick时被调用，其和process.nextTick()的区别在于两点：

　　　　1、所属的观察者被执行的优先级不一样，process.nextTick()属于idle观察者，setImmediate()属于check观察者，idle的优先级>check

　　 　  2、setImmediate()设置的回调函数是放置在一个链表中，每次Tick只执行链表中的一个回调。这是为了保证每次Tick都能快速地被执行
  
  
  # URL
## URL对象
### href
> 准备解析的完整的 URL，包含协议和主机（小写）
```
'https://user:pass@www.baidu.com:8080/order/productdetail?productId=234470&type=18#hash'
```

### protocol
> 请求协议， 小写
```
'https:'
```

### slashes
> 协议要求的斜杠（冒号后）
```
true 或 false
```

### host
> 完整的 URL 小写 主机部分，包含端口信息
```
www.baidu.com:8080
```

### auth
> url 中的验证信息
```
'user:pass'
```

### hostname
> 域名中的小写主机名
```
www.baidu.com
```

### port
> 主机的端口号
```
'8080'
```

### pathname
> URL 中的路径部分，在主机名后，查询字符前，包含第一个斜杠
```
'/order/productdetail'
```

### search
> URL 中的查询字符串，包含开头的问号
```
'?productId=234470&type=18'
```

### path
> pathname 和 search 连在一起
```
'/order/productdetail?productId=234470&type=18'
```

### query
> 查询字符串中得参数部分，或者使用 querystring.parse() 解析后返回的对象
```
'productId=234470&type=18' 或 {productId: 234470, type: 18}
```

### hash
> URL 的 “#” 后面部分（包括 # 符号）
```
'#hash'
```

## URL方法
### url.parse(urlStr[, parseQueryString][, slashesDenoteHost])
> 输入 URL 字符串，返回一个对象

*第二个参数parseQueryString（默认为false），如为false，则urlObject.query为未解析的字符串，比如author=%E5%B0%8F%E7%81%AB%E6%9F%B4，且对应的值不会decode；如果parseQueryString为true，则urlObject.**query为object**，比如{ author: '小火柴' }，且值会被decode*

*第三个参数slashesDenoteHos（默认为false），如果为true，可以正确解析不带协议头的URL，类似//foo/bar里的foo就会被认为是hostname；如果为false，则foo被认为是pathname的一部分*

### url.format(urlObject)
> url.parse(str)的反向操作，输入一个解析过的 URL 对象，返回格式化过的字符串

> urlObject包含了很多字段，比如protocol、slashes、protocol等，且不一定需要全部传，所以有一套解析逻辑

### url.resolve(from, to)
> url.resolve()方法以一种浏览器解析超链接的方式把一个目标URL解析成相对于一个基础URL，参数如下

> from <String> 解析时相对的基本 URL。  
  to <String> 要解析的超链接 URL。
```
url.resolve('/one/two/three', 'four') => /one/two/four
url.resolve('/one/two/three/', 'four') => /one/two/three/four
url.resolve('/one/two/three', '/four') => /four
url.resolve('http://example.com/', '/one') => http://example.com/one
url.resolve('http://example.com/one', '/two') => http://example.com/two
url.resolve('http://example.com/one', 'two') => http://example.com/two
url.resolve('http://example.com/one/', 'two') => http://example.com/one/two
```

# queryString
> nodeJS的queryString模块提供了一些处理 query strings 的工具

## 序列化
### querystring.parse(str[, sep[, eq[, options]]])
> querystring.parse()方法能把一个URL查询字符串(str)解析成一个键值对的集合，参数如下
```
str <String> 要解析的 URL 查询字符串。
sep <String> 用于界定查询字符串中的键值对的子字符串。默认为 '&'。
eq <String> 用于界定查询字符串中的键与值的子字符串。默认为 '='。
options <Object>
    decodeURIComponent <Function> 当解码查询字符串中百分号编码的字符时使用的函数。默认为 querystring.unescape()   
maxKeys <number> 指定要解析的键的最大数量。默认为 1000。指定为 0 则移除键数的限制
```
*[注意]querystring.parse()方法返回的对象不继承自 JavaScript 的 Object。 这意味着典型的 Object 方法如 obj.toString()、obj.hasOwnProperty() 等没有被定义且无法使用*

### querystring.stringify(obj[, sep][, eq][, options])
> querystring.stringify()方法是querystring.parse()方法的逆向操作，通过遍历对象的自有属性，从一个给定的obj产生一个URL查询字符串，参数如下
```
obj <Object> 要序列化成一个 URL 查询字符串的对象
sep <String> 用于界定查询字符串中的键值对的子字符串。默认为 '&'
eq <String> 用于界定查询字符串中的键与值的子字符串。默认为 '='
options
    encodeURIComponent <Function> 当把对URL不安全的字符转换成查询字符串中的百分号编码时使用的函数。默认为 querystring.escape()
```

## 编码
### querystring.escape(str)
> querystring.escape()方法对给定的 str 执行URL百分号编码，与encodeURIComponent方法一样

### querystring.unescape(str)
> querystring.unescape() 方法对给定的 str 上的URL百分号编码的字符执行解码，与decodeURIComponent方法一样

## GET
> get请求的数据保存在URL中
```
url: 'http://127.0.0.1:8080/home/test?a=1&b=2'
var http = require('http');
var url = require('url');
var querystring = require('querystring');
http.createServer(function(req,res){
    var urlObj = url.parse(req.url);
    var query = urlObj.query;
    var queryObj = querystring.parse(query);
    console.log(req.url);//'/home/test?a=1&b=2'
    console.log(query);//'a=1&b=2'
    console.log(queryObj);//{ a: '1', b: '2' }
}).listen(8080);
```

## POST
> post请求的数据会被写入缓冲区中，需要通过request的data事件和end事件来进行数据拼接处理
```
var http = require('http');
var url = require('url');
var querystring = require('querystring');
http.createServer(function(req,res){
    var str = '';  
    req.on('data', function(thunk){
        str += thunk;
    });
    req.on('end', function(){
        console.log(str);//'name=a&email=b%40b.com'
        var queryObj = querystring.parse(str);
        console.log(queryObj);//{ name: 'a', email: 'b%40b.com' }
    }); 

}).listen(8080);
```



## 包描述文件 package.json

### 基本字段

1. name——包名。规范定义它需要由小写的字母和数字组成，可以包含.、_和-，但不允许出现空格。包名必须是唯一的，以免对外公布时产生重名冲突的误解。除此之外，NPM还建议不要在包名中附带上node或js来重复标识它是JavaScript或Node模块 
2. version——版本号。一个语义化的版本号，这在http://semver.org/上有详细定义，通常为major.minor.revision格式

```
{
  "name": "my-n",
  "version": "1.0.0"
}
```

### 必需字段

1. description——包简介。方便别人了解该模块作用，搜索的时候也有用
2. keywords——关键词数组，NPM中主要用来做分类搜索
3. maintainers——包维护者列表。每个维护者由name、email和web这3个属性组成
4. contributors——贡献者列表, 列表中的第一个贡献应当是包的作者本人。它的格式与维护者列表相同
5. bugs——一个可以反馈bug的网页地址或邮件地址
6. licenses——当前包所使用的许可证列表，表示这个包可以在哪些许可证下使用
7. repositories——托管源代码的位置列表，表明可以通过哪些方式和地址访问包的源代码
8. dependencies——使用当前包所需要依赖的包列表。这个属性十分重要，NPM会通过这个属性帮助自动加载依赖的包
对应的版本可以加上各种限定，主要有以下几种：

    + 指定版本：比如1.2.2，遵循“大版本.次要版本.小版本”的格式规定，安装时只安装指定版本
    + 大于小于号(>或<)+指定版本：比如>=1.2.2，表示安装大于等于1.2.2的最新版本
    + 波浪号(tilde)+指定版本：比如~1.2.2，表示安装1.2.x的最新版本(不低于1.2.2)，但是不安装1.3.x，也就是说安装时不改变大版本号和次要版本号。
    + 插入号(caret)+指定版本：比如ˆ1.2.2，表示安装1.x.x的最新版本(不低于1.2.2)，但是不安装2.x.x，也就是说安装时不改变大版本号。需要注意的是，如果大版本号为0，则插入号的行为与波浪号相同，这是因为此时处于开发阶段，即使是次要版本号变动，也可能带来程序的不兼容
    + latest：安装最新版本

```
{
  "description": "node学习",
  "keywords": [],
  "maintainers": [
    {
      "name": "lff",
      "email": "lff@qq.com"
    }
  ],
  "contributors": [
    {
      "name": "lff",
      "email": "lff@qq.com"
    }
  ],
  "bugs": {
    "url": "https://github.com/lff/abc/def"
  },
  "licenses": [
    {
      "type": "MIT",
      "url": "https://github.com/napcs/node-livereload/blob/master/LICENSE"
    }
  ],
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/napcs/node-livereload.git"
  },
  "devDependencies": {
    "coffee-script": ">= 1.8.0",
    "mocha": ">= 1.0.3",
    "request": ">= 2.9.203",
    "should": ">= 0.6.3",
    "sinon": "^1.17.4"
  }
}
```

### 可选字段
1. homepage——当前包的网站地址
2. os——操作系统支持列表。这些操作系统的取值包括aix、freebsd、linux、macos、solaris、vxworks、windows。如果设置了列表为空，则不对操作系统做任何假设
3. cpu——CPU架构的支持列表，有效的架构名称有arm、mips、ppc、sparc、x86和x86_64。同os一样，如果列表为空，则不对CPU架构做任何假设
4. engine——支持的JavaScript引擎列表，有效的引擎取值包括ejs、flusspferd、gpsee、jsc、spidermonkey、narwhal、node和v8
5. builtin——标志当前包是否是内建在底层系统的标准组件
6. directories——包目录说明
7. implements——实现规范的列表。标志当前包实现了CommonJS的哪些规范
8. scripts——脚本说明对象。它主要被包管理器用来安装、编译、测试和卸载包。scripts指定了运行脚本命令的npm命令行缩写，比如start指定了运行npm run start时，所要执行的命令

```
{
  "homepage": "https://github.com/napcs/node-livereload#readme",
  "os": {},
  "cpu":{},
  "engines": {
   "node": ">=7.0",
   "npm": ">=4.0"
  },
  "directories": {}
}
```

### 其他字段
> 在包描述文件的规范中，NPM实际需要的字段主要有name、version、description、keywords、repositories、author、bin、main、scripts、engines、dependencies、devDependencies。与包规范的区别在于多了author、bin、main和devDependencies这4个字段
1. author——包作者
2. bin——指定各个内部命令对应的可执行文件的位置。一些包作者希望包可以作为命令行工具使用。配置好bin字段后，通过npm install package_name -g命令可以将脚本添加到执行路径中，之后可以在命令行中直接执行。通过-g命令安装的模块包称为全局模式
3. main——加载的入口文件
4. devDependencies——项目开发所需要的模块

```
  "bin": {
    "aa": "./bin/aa.js"
  },
  "main": "index.js",
  "devDependencies": {
    "coffee-script": ">= 1.8.0",
    "mocha": ">= 1.0.3",
    "request": ">= 2.9.203",
    "should": ">= 0.6.3",
    "sinon": "^1.17.4"
  }
```



### 代码展示

```
{
  "name": "my-n",
  "version": "1.0.0",
  "description": "node学习",
  "maintainers": [
    {
      "name": "lff",
      "email": "lff@qq.com"
    }
  ],
  "contributors": [
    {
      "name": "lff",
      "email": "lff@qq.com"
    }
  ],
  "bugs": {
    "url": "https://github.com/lff/abc/def"
  },
  "licenses": [
    {
      "type": "MIT",
      "url": "https://github.com/napcs/node-livereload/blob/master/LICENSE"
    }
  ],
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/napcs/node-livereload.git"
  },
  "devDependencies": {
    "coffee-script": ">= 1.8.0",
    "mocha": ">= 1.0.3",
    "request": ">= 2.9.203",
    "should": ">= 0.6.3",
    "sinon": "^1.17.4"
  },

  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev": "node index.js"
  },
  "author": "",
  "license": "ISC"
}
```



# Nodemon
> 修改代码后，需要重新启动 Express 应用，所做的修改才能生效。若之后的每次代码修改都要重复这样的操作，势必会影响开发效率，本文将详细介绍Nodemon，它会监测项目中的所有文件，一旦发现文件有改动，Nodemon 会自动重启应用

## 安装及使用
> 全局安装 nodemon 包，这样新创建的 Node.js 应用都能使用 Nodemon 运行起来了
```
npm install -g nodemon

nodemon index.js
```

## 配置文件
> Nodemon 默认会监听当前目录下（也就是执行 nodemon 命令所在的目录）的所有文件，不过有些情况下，虽然项目文件发生了改动，但是不需要 Nodemon 重启应用，那如何让文件不被 Nodemon 监听呢？不需要监听的文件，可以通过设置 Nodemon 的配置文件排除掉，新建文件 server/nodemon.json，添加代码：
一个配置文件可以被--config  <file>命令来指定
```
{
  "ignore": [
    "config.default.js"
  ]
}
```
> Nodemon 配置文件是 JSON 文件，通过设置 ignore 属性值，一个由文件名组成的字符串数组，指定不需要监听的文件

> 如果你想把所有的配置文件都配置在package.json中nodemon也是支持的，同样的格式但是必须在nodemonConfig标签下：
```
{
.........
"nodemonConfig":{
     "ignore":["test/*","docs/*"]
}
.........

}
```

## 指令解释
### nodemon -e 
>默认的 nodemon监视 .js, .mjs, .coffee,  litcoffee和Json文件，通过-e命令你可以指定你自己的查找列表：
```
nodemon -e js,jade
```
 这样nodemon会监视你的.js， .jade文件

### nodemon --watch path
> nodemon默认只会监视当前的工作路径，如果你想去监视其他路径上的文件，你可以使用如下命令：
```
nodemon --watch app --watch libs app/server.js
```

### nodemon --ignore
忽视一些文件被监视：
```
nodemon --ignore lib/app.js
```

### nodemon --delay
>有时候你会修改许多文件，这时为了避免不必要的重启，你可以通过此命令指定多少时间后再进行重启。
```
nodemon --delay 10 server.js
```

### 手动重启
 如果你的nodemon还在运行中，你想重启，你不需要关闭再重启，只需要
```
rs
```

## nodemon -h
> 查看帮助
 Options:
```
  --config file ............ alternate nodemon.json config file to use
  -e, --ext ................ extensions to look for, ie. js,jade,hbs.
  -x, --exec app ........... execute script with "app", ie. -x "python -v".
  -w, --watch path.......... watch directory "path" or files. use once for
                             each directory or file to watch.
  -i, --ignore ............. ignore specific files or directories.
  -V, --verbose ............ show detail on what is causing restarts.
  -- <your args> ........... to tell nodemon stop slurping arguments.
  ```
  


# events
>events模块是node的核心模块，几乎所有常用的node模块都继承了events模块，比如http、fs等。

## EventEmitter
> EventEmitter 类由 events 模块定义和开放的，所有能触发事件的对象都是 EventEmitter 类的实例

> events模块的EventEmitter属性指向该模块本身
```
events.EventEmitter === events  // true
```









