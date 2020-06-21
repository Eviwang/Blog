

# webpack  性能优化

- 有哪些方式可以减少 Webpack 的打包时间
- 有哪些方式可以让 Webpack 打出来的包更小





## 减少 Webpack 打包时间

###  优化 Loader

- 限定范围
- `loader: 'babel-loader?cacheDirectory=true'`限定babel编译过的缓存下来。

### HappyPack

### DllPlugin+DllReferencePlugin

## 其他：

## 1.noParse

```
module:{
    noParse:/jquery/, 不去解析jquery模块的依赖。加快打包速度
    rules:[
    
    ]
}
```

## 2.exlude,include

```
module:{
    rules:[
        test:/\.js$/
        exclude:/node_modules/,
        include:path.resolve("src")
    ]
}
```

## 3. webpack.IgnorePlugin

忽略掉某些库自带的一些包，比如`moment`的语言包。默认会把所有的语言包都加载进来。但是需要我们手动去引入需要的包。

```
//webpack.config.js
{
    plugins:[
        new webpack.IgnorePlugin(/\.\/locale/,/moment/)//moment库下的locale被忽略
    ]
}

// 手动引入
import 'moment/locale/zh-cn';
moment.locale('zh-cn')
```

## 4. 动态链接库 webpack.DllPlugin

1. 单独写一个

   ```
   webpack.config.js
   ```

   生成

   ```
   manifest.json
   ```

   ```
    entry: {
       vendor: ["react", "react-dom"]
    },
   output:{
       filename:'_dll_[name].js',
       library:'_dll_[name]',
       libraryTarget:'var'// commonjs,var,umd
   },
   plugins:[
       new webpack.DllPlugin({
           name:'_dll_[name]',//必须和library同名,实际上就是webpack打包后的js，前面加上var _dll_name = (/*webpack代码*/)
           path:path.resolve(__dirname,"dist","manifest.json")
       })
   ]
   ```

2. 页面中引入`<script>`

3. 配置manifest

```
{
    plugins:[
        new webpack.DllReferencePlugin({
            manifest:path.resolve("./dist/manifest.json")
        })
    ]
}
```

## happypack

多线程打包，适合大型项目的优化。小项目可能反而性能差。因为开启线程也是需要代价的。

```
rules:[
    {
        test:/\.js$/,
        use:'happypack/loader?id=js'//只用改写这里，指定用happypack的loader，并且指定id=js
    }
],
plugins:[
    new Happypack({
        id:"js",
        use:[
            //这里用上面的rule中的use
        ]
    })
]
```

## webpack自带优化

`production`模式：

- 使用`import`语法,默认会`tree-shaking`

- scope hosting作用域提升，默认语法优化。并且可以合并多个模块。

  ```
  module.exports = {
    optimization: {
      concatenateModules: true
    }
  }
  ```



## Webpack 打出来的包更小

### 按需加载

### Scope Hoisting

### Tree Shaking