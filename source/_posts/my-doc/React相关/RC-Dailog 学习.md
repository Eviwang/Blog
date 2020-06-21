RC-Dailog 学习

## rc-dialog

| animation          | String |      | part of dialog animation css class name 动画名字，有前缀的 |
| ------------------ | ------ | ---- | ---------------------------------------------- |
| maskAnimation      | String |      | part of dialog's mask animation css class name |
| transitionName     | String |      | dialog animation css class name  表示动画名字，没有前缀的  |
| maskTransitionName | String |      | mask animation css class name                  |
|                        |                                                       |       |                                                              |
| title                  | String\|React.Element                                 |       | Title of the dialog  只有传了才会显示Header                  |
| footer                 | React.Element                                         |       | footer of the dialog  只有传了才会显示Footer                 |
| closable               | Boolean                                               | true  | whether show close button                                    |
| mask                   | Boolean                                               | true  | whether show mask                                            |
| maskClosable           | Boolean                                               | true  | whether click mask to close   点击空白区域关闭弹框           |
| keyboard               | Boolean                                               | true  | whether support press esc to close                           |
| mousePosition          | {x:number,y:number}                                   |       | set pageX and pageY of current mouse(it will cause transform origin to be set). 动画运动的初始值 |
| onClose                | function()                                            |       | called when click close button or mask                       |
| afterClose             | function()                                            |       | called when close animation end                              |
| getContainer           | function(): HTMLElement \| IStringOrHtmlElement,false |       | to determine where Dialog will be mounted  ，如果为false，则渲染在当前dom，而不是用Portal的方式 |
| destroyOnClose         | Boolean                                               | false | to unmount child compenents on onClose                       |
| closeIcon              | ReactNode                                             |       | specific the close icon.                                     |
| forceRender            | Boolean                                               | false | Create dialog dom node before dialog first show  第一次就渲染 rc-root 元素，并且每次都渲染，不走lazyRender |
| focusTriggerAfterClose | Boolean                                               | true  | focus trigger element when dialog closed  解决弹框默认focs最后一个元素的bug |





## LazyRenderBox

```react
shouldComponentUpdate(nextProps: ILazyRenderBoxPropTypes) {
    if (nextProps.forceRender) {  // forceRender为true，则每次都渲染
      return true;
    }
    return !!nextProps.hiddenClassName || !!nextProps.visible;  // 如果visitble或者hiddenClassName被更新，则触发渲染。。
  }
```



更新原则：

- forceRender为true，则每次都渲染
- 如果visitble或者hiddenClassName有值，则触发渲染。。



## DialogWrap

包装类：

- 决定走`Portal` 或者直接渲染到当前元素节点

```react
<Rc-Dialog geContainner={false}></Rc-Dialog>
```

```react
<Rc-Dialog ></Rc-Dialog> 默认走的是Portal
```



## 技巧

- 给默认值：

```react
  
static defaultProps = {
    maskClosable: true,
    destroyOnClose: false,
    prefixCls: 'rc-dialog',
    focusTriggerAfterClose: true,
  };
```



- 找dom,  比如当前是一个React元素，可以找到子dom元素。`<LazyRenderBox ref={(ref)=>{ref}}></LazyRenderBox>`

  ```react
  const dialogNode = ReactDOM.findDOMNode(this.dialog);	如果用 ref 是获取组件的实例，而不是dom元素。	
  ```

- 利用  transform-origin  实现从鼠标点击的地方开始运行动画。





