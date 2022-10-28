---
title: 'js校验原生客户端日志开发'
date: 2022-10-28 10:54:42
tags: []
published: true
hideInList: false
feature: 
isTop: false
---
# video_js_template


## 工程编译与使用

### 工程编译

- 使用`./wbinit.sh`脚本，安装本工程需要的相关依赖；
- 使用`npm run webpack`，调用`./wbnpx.sh`脚本进行webpack打包；使用`node ./dist/bundle.js`可执行打包后的`bundle.js`文件；
- 使用`npm run build`，内部调用`./wbnpx.sh;./wbversion.sh build`脚本进行webpack打包，同时打出来的`bundle.js`会生成version版本变量，可使用`npm run build 2`来指定build号为2，不传build号则版本信息里的build号会自增；版本信息存储在`version.data`文件中；
- 使用`npm run release`，调用`./wbnpx.sh;./wbversion.sh release`脚本进行webpack打包，同时打出来的`bundle.js`会生成version版本变量，可利用`npm run release 1.0`命令指定版本号，如果不传版本号会展示最后一次的version号；
- 使用`npm run start`可启动`nodemon`服务，此服务会监听工程目录下的`/tscompile`文件夹文件的改动，若有更改时自动运行项目；
- 使用`npm run tscompile`触发编译或者`Command + shift + b`手动触发`tasks.json`任务，可编译/src/下的所有ts文件，把编译后的中间产物输出到`/tscompile`文件夹下，如果开启了`nodemon`服务，会自动触发nodemon的watch事件，触发热更新；配置了`launch.json`文件，可使用VSCode自带的`运行和调试（command + shift + D）`对项目中的具体代码进行断点和调试开发；
- 使用`npm run dev`，打开本地server，方便利用chrome调试；
- 终端 -> 运行任务 -> 显示所有任务 -> tsc:监视 - tsconfig.json，可以动态编译ts；


## 设计思路

### 整体流程

原生端上执行`bundle.js`代码，获取js运行环境，然后通过调用js函数并把当前日志json和这条日志对应的js模板代码作为参数，来对日志进行校验，js会返回校验的结果，端上根据返回结果做UI显示；

### 初步解决方案


## js校验api介绍

**校验工具暴露出的接口如下**

- `loadJSTemplate(code: string)`: 参数为动态下发的js文件的模板字符串；可把需要的js模板文件加载执行；
- `loadJsonTemplate(jsonString: string)`: 参数为下发的json格式的模板字符串；加载json模板；
- `checkFunction(log: string, context: string)`: 第一个参数为需要校验的json字符串，第二个参数为需要增量结合模板校验的context
- `loadJSTemplateAndExecute(code: string, log: string, context: string)`: 加载单个js模板，并立即执行校验
- `loadJsonTemplateAndExecute(jsonString: string, log: string, context: string)`: 加载单个json模板，并立即执行校验


## 工具脚本的使用

使用下面命令安装配套的脚本工具：

```

# 一键安装wbcompile.sh脚本
sudo curl http://ftp.client.weibo.cn/UI_Image/Video/ShellTools/installwbcompile.sh | sh

```

`wbcompile`脚本是具有处理新建日志模板、编译commonJS文件、上传ftp等功能，具体可通过`wbcompile -h`查看帮助命令；常用方法总结如下：

- `wbcompile -t templateName`可在当前执行脚本的目录下生成`templateName.ts`模板文件，可根据需求修改模板文件保存；
- `wbcompile -i inputFile(inputDir) -o outputDir` 或者 `wbcompile inputFile(inputDir) outputDir`命令对需要编译的文件进行编译，支持对typescript和ES6文件进行统一编译成ES5规范； -i 是需要编译的文件或文件夹，如果 -i 参数为文件夹，支持递归编译；-o 是编译后输出的文件路径；
- `wbcompile -u file`调用上传命令，上传编译好的ES5文件到ftp服务器；


## 日志模板的定义

| property | 含义 | 备注 |
| :------ | :------: | :------: |
| name | 需要校验的字段名，如uicode； |  |
| required | 是否是必须字段，即如果校验失败是否抛异常；默认是false； |  |
| sub | 如果验证的字段是复合型，比如ext字段，则支持多级嵌套； |  |
| logic | 逻辑关系，值含义枚举：0：表达式解析；1：包含；2：相等；3：正则；4：js函数； |  |
| rule | 和logic绑定关系，需要用来校验的rule； | logic为4时，rule为函数或者函数字符串，会调用rule函数来判断校验结果，参数为整个json转成的对象；logic为0或者不传时，默认使用表达式解析规则；可支持常用一元、二元操作符以及逻辑关系； |
|  |  |  |


## 遇到的问题和解决办法

- [x] 原生JSContext不支持执行多个 es6 js 文件，需要合并 es6 js 文件；
- [x] 使用webpack解决多个js文件合并问题，但是使用webpack的bundle.js文件是直接执行的匿名函数，一些export的方法名原生执行不到；
- [x] 编写wbnpx.sh脚本，对webpack生成的bundle.js文件做处理。匹配入口文件app.js中需要导出的对象，在bundle.js里直接写入；
- [x] 项目中js语法太过灵活，无法做类型定义，项目整体切换到typescript；
- [x] 单个js文件中可包含多个校验模板，模板和校验log逻辑拆分；
- [x] 利用eval()函数动态执行js文件字符串或者json模板字符串，可动态下发js代码执行；
- [x] 校验逻辑新增规则，可在js模板里定义一个function对象或者function字符串来进行校验，利用eval函数动态校验规则；同理json模板里也可返回function字符串；function的参数为json转成的对象；
- [x] 编写wbcompile.sh脚本，脚本可以生成模板文件，执行ts文件和es6文件转为es5文件，支持递归遍历子目录编译；支持直接上传ftp服务器；
- [x] 增加表达式解析规则，支持常用逻辑表达式解析，根据LL(1)递归下降词法算法编写解析器，读取输入表达式生成AST语法树，操作语法树节点运算校验；表达式支持一元、二元操作符，支持逻辑关系，支持变量的使用，示例如："(@mid === (1+2+3)*2-5) && (@source_info include 'face_sign_1')"
- [x] 编写版本管理脚本，记录每次build行为，保存为version.data便于读取；支持build号自增，支持指定release version；
