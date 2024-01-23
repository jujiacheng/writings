# webpack 基础使用

## webpack 是什么

webpack 是一个现代 JavaScript 应用程序的静态模块打包器，当 webpack 处理应用程序
时，会递归构建一个依赖关系图，其中包含应用程序需要的每个模块，然后将这些模块打包
成一个或多个 bundle。

## webpack 的核心概念

1. entry：指示 webpack 一那个文件为起点开始打包，分析构建内部依赖图。
2. output：指示 webpack 打包后的资源 bundles 输出到哪里去，以及如何命名。
3. loader：让 webpack 能够去处理那些非 JavaScript 文件(webpack 自身只能理解
   JavaScript)
4. plugins：插件可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一
   直到重新定义环境中的变量等。
5. mode：模式指示使用相应模式的配置。会将 DefinePlugin 中 process.env.NODE_ENV
   的值设置为 development 或 production。

## webpack 的基础使用

### 1.webpack 的安装

`npm install webpack@4.41.5 webpack-cli@3.3.10 -D` 安装完成后可以查看 webpack 的
版本号，命令行如下：

```JavaScript
npx webpack -v
npx webpack-cli -v
```

### 2.webpack 打包

从 wepack V4.0.0 开始， webpack 是开箱即用的，在不引入任何配置文件的情况下就可以
使用。 新建 src/index.js 文件，并写入一下代码：

```JavaScript
class Animal {
    constructor(name) {
        this.name = name;
    }
    getName() {
        return this.name;
    }
}

const dog = new Animal('dog');
```

使用 `npx webpack --mode=development` 进行构建，默认是 production 模式，我们为了
更清楚得查看打包后的代码，使用 development 模式。 可以看到项目下多了个 dist 目录
，里面有一个打包出来的文件 main.js。 webpack 有默认的配置，如默认的入口文件是
./src，默认打包到 dist/main.js。查看 dist/main.js 文件，可以看到，src/index.js
并没有被转义为低版本的代码，这显然不是我们想要的。

```JavaScript
{
    "./src/index.js":
        (function (module, exports) {

            eval("class Animal {\n    constructor(name) {\n        this.name = name;\n    }\n    getName() {\n        return this.name;\n    }\n}\n\nconst dog = new Animal('dog');\n\n//# sourceURL=webpack:///./src/index.js?");

        })
}
```

### 3.将 JS 转义为低版本

前面我们说了 webpack 的五个核心概念，其中之一就是 loader，loader 用于对源代码进
行转换，这正是我们现在所需要的。将 JS 代码向低版本转换，我们需要使用
babel-loader。首先我们安装一下 babel-loader：
`npm install babel-loader@8.2.5 -D` 此外，我们还需要配置 babel，为此我们安装一下
以下依赖:
`npm install @babel/core@7.18.10 @babel/preset-env@7.18.10 @babel/plugin-transform-runtime@7.18.10 -D`
`npm install @babel/runtime@7.18.9 @babel/runtime-corejs3@7.18.9` 新建
webpack.config.js，如下:

```JavaScript
//webpack.config.js
module.exports = {
    module: {
        rules: [
            {
                test: /\.jsx?$/,
                use: ['babel-loader'],
                exclude: /node_modules/ //排除 node_modules 目录
            }
        ]
    }
}
```

然后我们需要新建一个.babelrc 用来编写 babel 配置，具体如下：

```JavaScript
{
    "presets": ["@babel/preset-env"],
    "plugins": [
        [
            "@babel/plugin-transform-runtime",
            {
                "corejs": 3
            }
        ]
    ]
}
```

现在，我们重新执行 npx webpack --mode=development，查看 dist/main.js，会发现已经
被编译成了低版本的 JS 代码。

### 4.mode

小伙伴肯定也发现了，我们在使用 webpack 进行打包的时候，一直运行的都是 npx
webpack --mode=development 是否可以将 mode 配置在 webpack.config.js 中呢？显然是
可以的。这就需要用到 webpack 的核心配置项之一 mode，我们在 webpack.config.js 中
添加如下代码：

```JavaScript
module.exports = {
    //....
    mode: "development",
    module: {
        //...
    }
}
```

现在，我们直接使用 npx webpack 进行编译即可。

### 5.在浏览器中查看页面

搞了这么多我们还是不能在浏览器中查看页面，下面我么就来解决这个问题。 webpack 本
身无法对 html 进行打包处理，这时候我们需要使用 webpack 的另一个核心配置项
plugin。对于 html 我们用药的 plugin 是 html-webpack-plugin，首先我们安装一下插件
： `npm install **html**-webpack-plugin@4.5.0 -D` 新建 public 目录，并在其中新建
一个 index.html 文件( 文件内容使用 html:5 快捷生成即可)，修改 webpack.config.js
文件。

```JavaScript
//首先引入插件
const HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    //...
    plugins: [
        //数组 放着所有的webpack插件
        new HtmlWebpackPlugin({
            template: './public/index.html',
            filename: 'index.html', //打包后的文件名
            minify: {
                removeAttributeQuotes: false, //是否删除属性的双引号
                collapseWhitespace: false, //是否折叠空白
            },
            // hash: true //是否加上hash，默认是 false
        })
    ]
}
```

此时执行 npx webpack，可以看到 dist 目录下新增了 index.html 文件，并且其中自动插
入了
