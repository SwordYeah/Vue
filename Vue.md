# 11.8:

## Vue基础

### 前端工程化 

#### 实际的前端开发：

- 模块化（js 的模块化、css 的模块化、资源的模块化）
-  组件化（复用现有的 UI 结构、样式、行为）
-  规范化（目录结构的划分、编码规范化、接口规范化、文档规范化、 Git 分支管理）
-  自动化（自动化构建、自动部署、自动化测试）  

#### 前端工程化的解决方案  

目前主流的前端工程化解决方案：

- webpack（ https://www.webpackjs.com/ ）
- parcel（ https://zh.parceljs.org/ ）  

#### webpack 的基本使用  

##### 概念

​		webpack 是前端项目工程化的具体解决方案  

​		主要功能：它提供了友好的前端模块化开发支持，以及代码压缩混淆、处理浏览器端 JavaScript 的兼容性、性能优化等强大的功能。
​		好处：让程序员把工作的重心放到具体功能的实现上，提高了前端开发效率和项目的可维护性。
​		目前 Vue，React 等前端项目，基本上都是基于 webpack 进行工程化开发的  

![image-20221109105522466](D:\研二上\vue\images\Vue\image-20221109105522466.png)

在终端运行如下的命令，安装 webpack 相关的两个包：

~~~
npm install webpack@5.42.1 webpack-cli@4.7.2 -D  
~~~

##### 在项目中配置 webpack  

① 在项目根目录中，创建名为 webpack.config.js 的 webpack 配置文件，并初始化如下的基本配置：  

![image-20221109111041771](D:\研二上\vue\images\Vue\image-20221109111041771.png)

② 在 package.json 的 scripts 节点下，新增 dev 脚本如下：  

![image-20221109111059112](D:\研二上\vue\images\Vue\image-20221109111059112.png)

③ 在终端中运行 npm run dev 命令，启动 webpack 进行项目的打包构建  

##### mode 的可选值  

mode 节点的可选值有两个，分别是：
① development

- 开发环境

- 不会对打包生成的文件进行代码压缩和性能优化

-  打包速度快，适合在开发阶段使用  

② production

- 生产环境
- 会对打包生成的文件进行代码压缩 和性能优化
-  打包速度很慢，仅适合在项目发布阶段使用  

##### webpack.config.js 文件的作用  

​		webpack.config.js 是 webpack 的配置文件。webpack 在真正开始打包构建之前，会先读取这个配置文件，从而基于给定的配置，对项目进行打包。
​		由于 webpack 是基于 node.js 开发出来的打包工具，因此在它的配置文件中，支持使用 node.js 相关的语法和模块进行 webpack 的个性化配置。  

##### webpack 中的默认约定  

在 webpack 4.x 和 5.x 的版本中，有如下的默认约定：
① 默认的打包入口文件为 src -> index.js
② 默认的输出文件路径为 dist -> main.js
注意：可以在 webpack.config.js 中修改打包的默认约定  

​		**在 webpack.config.js 配置文件中，通过 entry 节点指定打包的入口。通过 output 节点指定打包的出口。  **

![image-20221109130054387](D:\研二上\vue\images\Vue\image-20221109130054387.png)



#### Webpack插件

最常用的
webpack 插件有如下两个：
① webpack-dev-server

- 类似于 node.js 阶段用到的 nodemon 工具
- 每当修改了源代码，webpack 会自动进行项目的打包和构建

② html-webpack-plugin
- webpack 中的 HTML 插件（类似于一个模板引擎插件）
- 可以通过此插件自定制 index.html 页面的内容  



#### webpack-dev-server

##### 配置 webpack-dev-server  

① 修改 package.json -> scripts 中的 dev 命令如下：  

![image-20221109133843440](D:\研二上\vue\images\Vue\image-20221109133843440.png)

② 再次运行 npm run dev 命令，重新进行项目的打包
③ 在浏览器中访问 http://localhost:8080 地址，查看自动打包效果  

##### 打包生成的文件位置

① 不配置 webpack-dev-server 的情况下，webpack 打包生成的文件，会存放到实际的物理磁盘上

- 严格遵守开发者在 webpack.config.js 中指定配置
- 根据 output 节点指定路径进行存放

② 配置了 webpack-dev-server 之后，打包生成的文件存放到了内存中

- 不再根据 output 节点指定的路径，存放到实际的物理磁盘上
- 提高了实时打包输出的性能，因为内存比物理磁盘速度快很多  



​		webpack-dev-server 生成到内存中的文件，默认放到了项目的根目录中，而且是虚拟的、不可见的。

- 可以直接用 / 表示项目根目录，后面跟上要访问的文件名称，即可访问内存中的文件
- 例如 /bundle.js 就表示要访问 webpack-dev-server 生成到内存中的 bundle.js 文件



​		**如果要实现实时加载，那么在html文件中需要需改引用文件的位置，如原来是./dist/hello.js,那么要改成根目录加文件名，即/hello.js**



#### html-webpack-plugin  

​		html-webpack-plugin 是 webpack 中的 HTML 插件，可以通过此插件自定制 index.html 页面的内容。  

##### 配置

​		在webpack.config.js中添加以下内容：

![image-20221109135259118](D:\研二上\vue\images\Vue\image-20221109135259118.png)