浏览器开发文档
--------

http://nodejs.cn/api/

*   electron文档
https://electronjs.org/docs

    1.安装nodejs http://nodejs.cn/
    2.安装cnpm yarn作为库管理器 npm install -g cnpm yarn
    3.使用cnpm 安装electron全局库 cnpm install -g electron

*   nodejs第三方库查找与安装方法
    全局库以electron为例:   cnpm install -g electron
    本地库以typescript为例: yarn add typescript
    
    安装多个库: 
        cnpm install -g [库1] [库2] ...
        yarn add [库1] [库2] ...
    
    安装开发库(不会被打包到最终代码中):
        yarn add -D [库1] [库2] ...
    
*   electron: Hello World示例
    初始化一个项目:
    mkdir helloworld && cd helloworld
    yarn init -y
    mkdir src

    添加依赖库:
    yarn add electron

    修改配置:
    将package.json中的main属性 改为src/index.js
    
    拷贝代码index.js 与 helloworld.html 到 src 目录下
    在与package.json文件目录下执行命令行 electron .

*   文件结构：
    - src 源码目录
        - index.js
        - helloworld.html
    - package.json 项目工程配置
    - yarn.lock 库版本锁定文件(需要git忽略)
    - node_modules 第三方本地库存放目录(需要git忽略)

*   源码(使用javascript es6 规范):
index.js
```javascript
const path = require("path");   //path内置库
const {app, BrowserWindow} = require("electron");   //electron开发库

let mainWindow;     //窗口对象

//注册app ready事件
app.on("ready", ()=>{
    mainWindow = new BrowserWindow({
        width: 800,
        height: 600,
        show: true
    });

    mainWindow.webContents.openDevTools();
    mainWindow.loadFile(path.resolve(__dirname, "helloworld.html"));
});

//当所有窗口关闭时退出程序
app.on("window-all-closed", ()=>{
    app.quit();
});
```

helloworld.html
```html
<html>
    <head>
        <!--此处标题会直接设置到应用-->
        <title>Hello World</title>
    </head>
    <body>
        <h1>
            Hello World
        </h1>
    </body>
</html>
```
