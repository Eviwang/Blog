---
title: 从零开始配置一个webpack-vue项目
date: 2018-05-29 15:53:45
tags: [webpack,vue]
---



## 安装 VSCode 插件
- AutoClose Tag
- Auto Rename Tag
- Beautify
- EditorConfig for VS code
- git history
- html css support
- ESLint
<!-- more -->
- gitignore
- language-stylus
- Path Intellisense
- Nunjucks
- One Dark Pro
- PostCSS syntax
- vue
- vue 2 Snippets
- Vetur
- View In Browser
- vscode-icons



## VSCode 配置

```
{
    // "window.zoomLevel": 0,
    // "editor.fontSize": 15,
    "vsicons.projectDetection.disableDetect": true,
    "workbench.iconTheme": "vscode-icons",
    "files.autoSave": "onFocusChange",
    "files.exclude": {
        "**/*.js":{ "when": "$(basename).ts"},
        "**/*.js.map": { "when": "$(basename)"},
        "**/*.gitkeep":true,
        "node_modules":true
    },    
    "update.channel": "none"
}

```

 ## 开启项目
 
```
npm init
cnpm i vue -S
cnpm i webpack webpack-cli webpack-dev-server vue vue-loader -D
cnpm i css-loader vue-template-compiler -D
cnpm i babel-loader vue-style-loader -D
cnpm i style-loader url-loader file-loader -D
cnpm i stylus-loader stylus -D
cnpm install cross-env webpack-dev-server -D 
/*cross-env 解决windows与其他操作系统设置环境变量的问题，
windows下需要用 set NODE_ENV，使用："build":cross-env NODE_ENV="production" webpack*/
cnpm install html-webpack-plugin -D

cnpm i webpack webpack-cli vue vue-loader css-loader vue-template-compiler babel-loader vue-style-loader url-loader file-loader stylus-loader stylus -D
```




## 创建文件

```
//1. 创建 webpack.config.js
var Path = require("path");
const { VueLoaderPlugin } = require('vue-loader');

module.exports = {
    entry:"./src/index.js",
    output:{
        filename:"index.js",
        path:Path.join(__dirname,"/dist/")
    },
    module:{
        rules:[
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
            {
                test: /\.js$/,
                loader: 'babel-loader'
            },
            {
                test: /\.css$/,
                use: [
                    'vue-style-loader',
                    'css-loader'
                ]
            }
        ]
    },
    plugins:[
        new VueLoaderPlugin()
    ]
}

//2. 创建 src/app.vue

<template>
  <div id="txt">
      {{txt}}
  </div>
</template>


<script>
export default {
    data(){
        return {
            txt:"hello world!"
        }
    }
}
</script>


<style>
#txt{
    color:red;
}
</style>


//3. 创建 src/index.js
import Vue from "vue";
import App from "./app.vue";


var root = document.createElement("div");
document.body.appendChild(root);


new Vue({
        render(h){
            return h(App);
        },
    }
).$mount(root);

//4. 添加 npm script
"build": "webpack --mode development"
```




### 使用webpack-dev-server

```
cnpm install cross-env webpack-dev-server -D
// 添加script:
"dev":"webpack-dev-server --mode development";

devServer : {
    port:8000,
    host:"0.0.0.0",
    hot:true,
    overlay:{
        errors:true,//将错误显示到网页
    }
},

```

### 运行
```
npm run build
npm run dev
```

## 添加插件
```
cnpm install html-webpack-plugin -D

```

### 最终webpack.config.js
```javascript
var Path = require("path");
const { VueLoaderPlugin } = require('vue-loader');
const HtmlWebpackPlugin = require("html-webpack-plugin");
var webpack = require("webpack");

module.exports = {
    entry:"./src/index.js",
    output:{
        filename:"index[hash].js",
        path:Path.join(__dirname,"/dist/")
    },
    module:{
        rules:[
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
            {
                test: /\.js$/,
                loader: 'babel-loader'
            },
            {
                test: /\.css$/,
                use: [
                    'vue-style-loader',
                    'css-loader'
                ]
            },
            {
                test:/\.styl$/,
                use:[
                    "style-loader",
                    "css-loader",
                    "stylus-loader",
                ]
            },
            {
                test:/\.(gif|jpg|jpeg|png)/,
                use:[
                    {
                        loader : "url-loader",
                        options:{
                            limit:1024,
                            name:"[name]-test.[ext]"
                        }
                    }
                ]
            }
        ]
    },
    devServer : {
        port:8000,
        host:"0.0.0.0",
        hot:true,
        overlay:{
            errors:true,//将错误显示到网页
        }
    },
    plugins:[
        new VueLoaderPlugin(),
        new HtmlWebpackPlugin(),
        new webpack.HotModuleReplacementPlugin()
    ]
}


```

## 1.使用webpack-merge拆分，webpack.config

使用 merge.smart()

```javascript
// base.config.js
const Path = require("path");
const webpack = require("webpack");
const { VueLoaderPlugin } = require('vue-loader');
module.exports = {
    entry:{
        app:"./src/index.js"
    },
    output:{
        filename:"index.js",
        path:Path.join(__dirname,"../dist/")
    },    
    module:{
        rules:[
            {
                test: /\.vue$/,
                loader: 'vue-loader'
            },
            {
                test: /\.js$/,
                loader: 'babel-loader'
            },
            {
                test: /\.css$/,
                use: [
                    'vue-style-loader',
                    'css-loader'
                ]
            },
            {
                test: /\.(gif|jpg|jpeg|png|svg)$/,
                use: [
                  {
                    loader: 'url-loader',
                    options: {
                      limit: 1024,
                      name: 'resources/[path][name].[hash:8].[ext]'
                    }
                  }
                ]
              }
        ]
    },
    plugins:[
        new VueLoaderPlugin(),
    ]
}

```


```javascript
// client.config.js
const path = require('path')
const HTMLPlugin = require('html-webpack-plugin')
const webpack = require('webpack')
const merge = require('webpack-merge')
const ExtractPlugin = require('extract-text-webpack-plugin')
const baseConfig = require('./webpack.config.base')

const isDev = process.env.NODE_ENV === 'development';


console.log(process.env.NODE_ENV);

const defaultPluins = [
  new webpack.DefinePlugin({
    'process.env': {
      NODE_ENV: isDev ? '"development"' : '"production"'
    }
  }),
  new HTMLPlugin()
]

const devServer = {
  port: 8000,
  host: '0.0.0.0',
  overlay: {
    errors: true
  },
  hot: true
}

let config;

if (isDev) {
  config = merge(baseConfig, {
    module: {
      rules: [
        {
          test: /\.styl/,
          use: [
            'vue-style-loader',
            'css-loader',
            {
              loader: 'postcss-loader',
              options: {
                sourceMap: true
              }
            },
            'stylus-loader'
          ]
        }
      ]
    },
    resolve:{
        alias: {
            'vue$': 'vue/dist/vue.esm.js' // 在 webpack 1 中使用 'vue/dist/vue.common.js'
          }
    },
    devServer,
    plugins: defaultPluins.concat([
      new webpack.HotModuleReplacementPlugin(),
    ])
  })
} else {
  config = merge(baseConfig, {
    entry: {
      app: path.join(__dirname, '../src/index.js'),
    },
    output: {
      filename: '[name].[chunkhash:8].js',
    },
    resolve:{
        alias: {
            'vue$': 'vue/dist/vue.esm.js' // 在 webpack 1 中使用 'vue/dist/vue.common.js'
          }
    },
    module: {
      rules: [
        {
          test: /\.styl/,
          use: ExtractPlugin.extract({
            fallback: 'vue-style-loader',
            use: [
              'css-loader',
              {
                loader: 'postcss-loader',
                options: {
                  sourceMap: true
                }
              },
              'stylus-loader'
            ]
          })
        }
      ]
    },
    plugins: defaultPluins.concat([
      new ExtractPlugin('styles.[contentHash:8].css')
    ])
  })
}

module.exports = config

```

## 2. 使用vue-loader

```
// vue-loader 16.0.0 已经移除了下面选项
// vue-loader.config.js
module.exports = (isDev) => {
  return {
    preserveWhitepace: true,//处理vue template时，手误多打了空格问题
    extractCSS: !isDev,
    cssModules: {
      localIdentName: isDev ? '[path]-[name]-[hash:base64:5]' : '[hash:base64:5]',
      camelCase: true
    },
    // hotReload: false, // 根据环境变量生成
  }
}

// webpack.base.config.js
const createVueLoaderOptions = require('./vue-loader.config');

{
    test: /\.vue$/,
    loader: 'vue-loader',
    options: createVueLoaderOptions(isDev)
}
```

## 3.使用css-module
- 在vue-loader里面配置：

```
module.exports = (isDev) => {
  return {
    cssModules: {
      localIdentName: isDev ? '[path]-[name]-[hash:base64:5]' : '[hash:base64:5]',//线上生成的css名更短，有命名空间
      camelCase: true //将css中的 main-header转换为camelCase
    },
  }
}

// 在.vue中使用：
<style module>//加上module
.main-header{
    color:red;
}

</style>
<template>
<div :class="$style.mainHeader">//用这种绑定的方式，而且是camcase的
</div>
</template>

```

- vue-loader 15.0
```
// webpack.config.js -> module.rules
{
  test: /\.scss$/,
  use: [
    'vue-style-loader',
    {
      loader: 'css-loader',
      options: { modules: true }//重点
    },
    'sass-loader'
  ]
}
```



- 在css-loader里面配置

```
rules: [
    {
      test: /\.styl/,
      use: [
        'vue-style-loader',
        'css-loader',
        {
          loader: 'postcss-loader',
          options: {//添加这里
            module:true,
            localIdentName: isDev ? '[path]-[name]-[hash:base64:5]' : '[hash:base64:5]',
          }
        },
        'stylus-loader'
      ]
    }
]
```


## 4.使用ESlint

```
cnpm i eslint eslint-config-standard eslint-plugin-standard eslint-plugin-promise eslint-plugin-import eslint-plugin-node -D


//创建 .eslintrc
{
    "extends":"standard",
    "plugins":[
        "html"
    ]
}
cnpm i eslint-plugin-html -D//校验html中 script标签里面js

//添加npm script
"lint":"eslint --ext .js --ext .jsx --ext .vue client/"//检查client文件夹下的 js,jsx,vue文件

//添加 eslint自动修复
"lint-fix":"eslint --fix --ext .js --ext .jsx --ext .vue client/"

//让每次保存都去检查语法
cnpm install eslint-loader babel-eslint -D
//在.eslintrc文件中加入
"parser":"babel-eslint" //让eslint支持bable的语法

// 在webpackconfig.js中添加loader
{
    test: /\.(vue|js|jsx)$/,
    loader: 'eslint-loader',
    exclude: /node_modules/,
    enforce: 'pre' //在其他这几种文件的loader处理之前，都先用eslint-loader处理
},


```

## 5.添加.editorconfig文件
需要安装插件，EditorConfig for VS Code 这个是针对于编辑器的vscode等等

```
root = true

[*]
charset = utf-8
end_of_line = lf
indent_size = 2
indent_style = space
insert_final_newline = true
trim_trailing_whitespace = true
```

## 6.在git提交时，进行eslint语法检查

```
//需要 git init,保证你的git是可用的，然后再安装插件husky
执行命令 git init


cnpm i husky -D

//添加npm script,当git提交时，husky会自动会调用precommit命令
"precommit":"npm run lint"//任选一个，一个会fix，一个不会fix
"precommit":"npm run lint-fix"


```

7. 使用 rimrf清理dist目录

```
build:"npm run clean && npm run build:client"
clean:"rimraf dist"
```


