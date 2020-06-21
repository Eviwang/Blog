TDD

1. 编写测试用例
2. 运行测试，测试 无法通过测试
3. 编写代码，使测试用例通过测试
4. 优化代码，完成开发
5. 重复



TDD的优势

1. 长期减少回归bug
2. 代码质量好（组织，可维护性）
3. 测试覆盖率高（80%是很容易的，但是从80-100可能会花费之前的2倍或者几倍，一般是取一个平衡点）
4. 错误测试代码不容易出现



## 实战

```javascript
create-react-app demo
npm run eject



```

默认是有一些jest的配置在 package.json中的，但是我们可以将jest.config.js 独立出来

然后运行 npm run test



## 使用[enzyme](<https://github.com/airbnb/enzyme>)

首先安装包，然后在   `setuptest.js`文件中加入：

```javascript
import Enzyme from 'enzyme';
import Adapter from 'enzyme-adapter-react-16';

Enzyme.configure({ adapter: new Adapter() });

```

[shallow api ](<https://github.com/airbnb/enzyme/blob/master/docs/api/shallow.md>)

常用：

- find("[data-test='header'") // 使用data-test避免和代码耦合
- simulate("keyUp",{ keyCode:13 })`
- `simulate("change",{ target:{ value : 33 } })`
- setState({ value: "hello"});
- prop("value") 访问原生dom的值

目录结构 ：

```
│  index.js
│
├─Head
│      index.js
│
├─TodoList
└─__tests__ // 就近新建一个测试文件夹
    └─unit  // 单元测试
            head.js
```



测试change方法：

```javascript
test('测试 onChange', () => {
  const wapper = shallow(<Header />);
  const selector = '[data-test="input"]';
  const input = wapper.find(selector);
  const newValue = '888';
  input.simulate('change', {
    target: {
      value: newValue
    }
  });
    
  // 这里是用react 的state方式 测试，用数据来表达。单元测试推荐用这种
  expect(wapper.state('value')).toBe(newValue);
  // 这里用原生dom的方式测试。  集成测试用这种方式
  expect(wapper.find(selector).prop('value')).toBe(newValue);
});
```



```javascript
test('onAddItem 应该被渲染', () => {
  const wapper = shallow(<TodoList />);
  const newValue = '666';
  wapper.instance().onAddItem(newValue);
  expect(wapper.state('todoList').length).toBe(1);

  expect(wapper.find('ul').text()).toContain(newValue);
});

```

- toHaveBeenLastCalledWith("input")
- (wrapper.state("list").length).toBe(2)
- wrapper.find("Header") //可以直接找到Header组件
- wrapper.props("value") 取到传进来的props.value



## 快照

```
const wrapper = shallow(<Button></Button);
wrapper.toMatchSnapshot();
```



## 什么时候引入自动化测试

写单元测试确实很费时间，我们可以做一些取舍，在下面几种场景特别适合：

- 重构的时候，非常困难，要一次次手动点击。回归测试，非常费时间。

- 在核心功能开发的时候引入自动化测试非常有必要



## 测试覆盖率

statement  是代码声明

branch 是分支



## TDD

TDD只是一种模式，并不代表就是单元测试。也可以是集成测试。

- 好处：

  代码质量高

## 单元测试

- 测试覆盖率高
- 业务耦合度高
- 代码量大
- 过于独立

适用于 函数库。所以shallow适合单元测试。



## 集成测试 DDD

适用于业务，更加的，稳定性高

一般先写实现

然后写集成测试代码，模拟用户行为



## 对比

![1583246174507](F:\my-code\my-blog\Blog\source\_posts\my-doc\TDD-BDD\TDD\1583246174507.png)







## 引入Redux会对BDD有什么影响

测试中只需要引入Provider和Store就行了，代码变动量很小



## 实践项目如何运用

可以同时写，利用各自的优点。

一个好的项目自动化测试，并不是只能运用一种。











