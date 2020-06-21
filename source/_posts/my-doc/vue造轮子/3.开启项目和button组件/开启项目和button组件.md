1. 在github创建项目
2. npm init -y
3. 添加 .gitignore
4. 推送到远程分支
5. 创建licence    打开github 点 `Create New File` -> `输入Licence`会弹出选择 模板

如何选择协议：

![img](http://www.ruanyifeng.com/blogimg/asset/201105/bg2011050101.png)



##  使用git-open

`npm i -g git-open`

然后  在命令行使用 : `git open` 可以快速打开网站切换到当前分支。



## 使用 parcel

看文档



## 使用css变量

```css
:root {
  --button-height: 32px;
  --font-size: 14px;
  --button-bg: white;
  --button-active-bg: #eee;
  --border-radius: 4px;
  --color: #333;
  --border-color: #999;
  --border-color-hover: #666;
}
.g-button{
    background:var(--button-bg)
}
```



## 使用icon font

<https://www.iconfont.cn/>

加入购物车

在下载时选择 `symbol `  左上角，生成js，这样可以使用svg的图标

在项目中引入js

配置前缀【更多操作】->【编辑项目】

使用 `fill:red` 改变颜色

在项目中使用 图标 ，并设置 宽和高：

```html
<svg class="icon" v-if="icon">
    <use :xlink:href="`#icon-i-${icon}`" />
</svg>
.icon {
  width: 1em;
  height: 1em;
}
```



##  css知识点

- 使用flex布局，让图标对齐
- 使用`vertical-align:bottom`让每个button对齐
- 使用 `order:2` 技巧让图标在左或者在右
- 使用动画制作loading效果



## ButtonGroup知识点

- 组件不能直接为`<slot>`

- 如何做校验，确保g-button-group的子元素一定是 g-button

- `margin-left:-1px`去除重复边框 和 `:first,:last,not(first-child)` 的妙用

  