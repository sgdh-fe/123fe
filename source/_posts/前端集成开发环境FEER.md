---
title: 前端集成开发环境 FEER
date: 2020-06-12 09:21:26
categories: js
tags:
- 开发环境
- RollupJS
author: kun
---

<style type="text/css">
    .br10{border-radius: 6px;}
</style>

<img class="br10 k-lazy" src="./f_02.jpg">


<!-- more -->


**`Feer`** 基于[RollupJS](https://www.rollupjs.com/) 打造的前端工具集成环境. [Github](https://github.com/consolejs/feer-cli) &ensp;🚀 

> 命名灵感来自 **`F`** ront- **`E`** nd&ensp; Engine **`er`**, 即前端工程构建师 `FEer`, 类似`PHPer`、`JAVAer` 


<p align='center'>
  <img class="br10 k-lazy" src='./screenshot.svg' width='640'>
</p>


## 安装 & 使用

### 命令行

- 全局安装
```bash
npm i feer-cli -g
```
- 默认使用
```
feer <project-name>
```
- 或者
```bash
npx feer-cli <project-name>
```

### 场景支持 

在使用 `feer` 命令创建过程中，会提供模板选择功能, 支持 `PC`和`H5` :

```bash
? Which type do you want to create? (Use arrow keys)
❯ PC - (build the pc page)
  H5 - (build the h5 page)
```

<br>

## 文件目录

```c
├── .babelrc ---> babel配置文件
├── .gitignore ---> git过滤规则
├── .eslintrc ---> ESLint配置
├── .eslintignore ---> ESLint过滤规则
├── README.MD
├── package.json
├── build ---> 打包文件夹
├── config ---> 配置文件夹(`*`)
├── views ---> Nunjucks 模板引擎
├── imgs ---> 图片资源文件 (使用cdn时，可删除该文件夹)
└── src ---> 源代码文件夹
```

### config 配置

```c
├── build.js ----> nunjucks模板处理
├── server.js ----> fastify静态服务器、路由处理
└── rollup.config.js ---> RollupJS配置文件, 内可配置环境变量
```

### src 代码资源

```c
├── libs ---> 可存放引入的第三方库文件
├── mods ---> 各模块业务逻辑
├── index.js ---> 入口文件index.js
└── styles ---> scss 源代码文件夹, 可自定义
```

### views 模板文件

```c
├── common ---> 存放公共模板, 如parent、header、footer等
├── mods ---> 各个模块业务模板
└── index.html ---> 主页面模板, 可结合路由自定义配置其他页面
```

### build 编译输出

```c
├── index.html ---> html模板文件
├── js ---> js源代码文件夹
├── css ---> css资源文件
└── img ---> 图片资源文件 (使用cdn时，可删除该文件夹)
```

<br>

---

## 关键特性

* 基于`RollupJS`快速打包，让bundle最小化
* Tree-shaking帮助你移除无用代码
* 支持单/多页面开发
* 支持Proxy代理访问接口
* 基于MockJS 模拟 api
* 配置简单便捷、打包迅速
* Nunjucks, 功能丰富、强大的模板引擎
* 支持Sass、Less强大的CSS扩展语言
* 可灵活配置路由
* ES6书写优雅的JS代码
* 支持自动打开浏览器(自动获取本地的ip地址)
* 历经多个项目考验、不断改进升级
* 可兼容支持ie6、7+

***

<br>


## 关于配置

### Rollup 简介

**[Rollup](https://www.rollupjs.com/)**是一个JavaScript模块打包利器，<u>它使用的ES6模块标准</u>，代替像CommonJS和AMD的模块加载方案，即意味着开发者可以<u>直接使用import和export来优雅地书写代码</u>，且无需要引入*日常必备*工具**Babel**了。Rollup可以优化ES模块，以现代浏览器中实现更快地加载。

另外，还有一个重要亮点叫做"`Tree-shaking`"，通过这个特性可以帮助开发者从最终的编译文件中<u>排除任何未使用的代码</u>。该特性是基于ES6模块的静态分析，保证最终打包代码的纯净。<u>且不会增加额外的依赖</u>，Webpack虽然也可实现，但配置复杂且造成打包后臃肿。

### 插件使用

#### 基础包

```
rollup-plugin-node-resolve ----->帮助Rollup查找外部模块并导入
rollup-plugin-commonjs  --->将CommonJS模块转换为ES6提供给Rollups使用
rollup-plugin-babel ---> 使用es6新特性来书写代码
rollup-plugin-uglify ---> 压缩还可使用 pure_funcs移除console等
rollup-plugin-eslint ---> 必不可少的代码检测
```

#### 热选包

```
rollup-plugin-postcss --> Rollup和PostCSS间的无缝集成
rollup-plugin-livereload ---> 热更新~
rollup-plugin-copy --> 用来复制文件和文件夹，支持glob
```

### Web服务

[`Fastify`](https://github.com/fastify/fastify) 是一个高度专注于以最少开销和强大的插件架构为开发者提供最佳体验的 Web 框架。

**Fastify** 快速并且低开销，且专为 Node.js 平台量身打造,
它受到了Hapi和Express的启发， 是目前最快的Node框架之一。

> 见`config/server.js`，也可详细[API文档](https://lavyun.gitbooks.io/fastify/content/Getting-Started.html)


#### 特性

* 高性能：每秒可以提供 76k+个请求
* 可扩展：Fastify 通过其钩子，插件和装饰器完全可扩展
* 基于模式：可使用 JSON Schema 来验证路由并序列化输出
* 日志记录：输出日志
* 对开发者友好：该框架构建非常有表现力，不牺牲性能和安全性

#### 使用

重点在如下四个方面的使用：

1. **模板渲染**，借助插件[point-of-view](https://github.com/fastify/point-of-view)，除了 Nunjucks, 对ejs、pug、以及twig等，均可支持。

```js
fastify.register(require("point-of-view"), {
  engine: {
    nunjucks: require("nunjucks")
  }
});

```


2. **启用静态服务**，默认为4000端口

```js
// 启用静态服务，4000端口
const port = 4000;
fastify.listen(port, ip4, (err, address) => {
  if (err) throw err;
});
```

3. **路由配置**，方便、灵活

```js
// 配置router方法
function configRouter(name) {
  // 若默认为空 ''，指向 index文件
  fastify.get("/" + name, (req, reply) => {
    reply.view((name == "" ? "index" : name) + ".html", {});
  });
}

// 路由名字,首页一般为空 '/'
const routerNames = ["", "index"];

// 执行配置
for (let i in routerNames) {
  configRouter(routerNames[i]);
}
```

4. **Proxy** 跨域代理接口

```js
// proxy
const pathname = "/api/";
fastify.get(pathname, async (request, reply) => {
  reply.type("application/json").code(200);
  const url = new URL("https://jsonplaceholder.typicode.com/todos/1");
  const query = request.query;
  Object.keys(request.query).forEach(key =>
    url.searchParams.append(key, query[key])
  );
  const body = await fetch(url).then(res => res.json());
  return body;
});
```

### 模板引擎

[`Nunjucks`](https://mozilla.github.io/nunjucks/) 是 JavaScript 专用的功能丰富、强大的模板引擎。

由`Mozilla`开发的一个纯JS编写的模板引擎，既可以用在Node环境下，又可以运行在浏览器端。

`Nunjucks` 的 API 包括渲染模板，添加过滤器和扩展，自定义模板加载器等等。  


#### 优点

* __功能丰富且强大__，并支持块级继承（block inheritance）、自动转义、宏（macro）、异步控制等等。
* __快速 & 精简 并且高效__。运行时代码经过压缩之后只有 8K 大小， 可在浏览器端执行预编译模板。
* __可扩展性超强__，用户可以自定义过滤器（filter）和扩展模块。
* __随处可运行__，无论是 node 还是任何浏览器都支持，并且还可以预编译模板。

#### 使用

`Nunjucks` 内置了大量**标签**，它们是一些特殊的区块，可以对模板执行一些操作。

如：if、for 等分支语句，与 javascript 中的 if、for 类似。

> 小注： for 一样可以遍历数组 (arrays) 和对象 (dictionaries)。

```js
{% if variable %}
  It is true
{% endif %}

{% for i in [1,2,3,4] %}
  {{ i }}
{% endfor %}
```

**模板继承** 能让你以更强大的方式复用模板。通过定义父模板的基本结构然后由子模板来填充内容。
```html
{% extends "parent.html" %}

{% block header %}
    <h3>{{ subtitle }}</h3>
{% endblock %}

{% block content %}
    <h1>{{ page.title }}</h1>
    <p>{{ page.content }}</p>
{% endblock %}
```

**宏** (macro) 可以定义可复用的内容，类似与编程语言中的函数，看下面的示例：

``` html
{% macro field(name, value='', type='text') %}
<div class="field">
  <input type="{{ type }}" name="{{ name }}"
         value="{{ value | escape }}" />
</div>
{% endmacro %}
```
现在 `field` 可以当作函数一样使用了：

```js
{{ field('user') }}
{{ field('pass', type='password') }}
```

还有很多好玩又方便的api，更多详见 [API文档](https://mozilla.github.io/nunjucks/cn/templating.html)