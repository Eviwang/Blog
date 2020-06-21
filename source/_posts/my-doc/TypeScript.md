# TypeScript

## 类型

### 枚举

枚举可以定义静态方法。





## lib.d.ts

安装ts的时候，默认定义了这个ts文件。

对lib里面的类型进行扩展：

```c#

interface Window {
  helloWorld(): void;
}

interface String {
  endsWith(suffix: string): boolean;
}
```

### [终极string](<https://jkchao.github.io/typescript-book-chinese/typings/lib.html#%E7%BB%88%E6%9E%81-string>)

推荐创建一个`global.d.ts`

```c#
// 确保是模块
export {};

declare global {
  interface String {
    endsWith(suffix: string): boolean;
  }
}

String.prototype.endsWith = function(suffix: string): boolean {
  const str: string = this;
  return str && str.indexOf(suffix, str.length - suffix.length) !== -1;
};

```

### [--lib选项](<https://jkchao.github.io/typescript-book-chinese/typings/lib.html#lib-%E9%80%89%E9%A1%B9>)





## Callable

```c#
可以被调用：
interface ReturnString {
  (): string;
}
// 等价： type ReturnString : ()=>string;
declare const foo: ReturnString;
const bar = foo(); // bar 被推断为一个字符串。
```



### 实例化

```c#
interface CallMeWithNewToGetString {
  new (): string;
}
```





## 类型保护

在编写`if-else`的时候会有类型推断和约束

- typeof

- instanceof

- in

- [字面量保护](<https://jkchao.github.io/typescript-book-chinese/typings/typeGuard.html#%E5%AD%97%E9%9D%A2%E9%87%8F%E7%B1%BB%E5%9E%8B%E4%BF%9D%E6%8A%A4>)

- 使用定义的类型保护

  - ```c#
    // 用户自己定义的类型保护！
    function isFoo(arg: Foo | Bar): arg is Foo {
      return (arg as Foo).foo !== undefined;
    }
    ```



## 字面量类型

- 字符串   

  - ```typescript
    let foo: 'Hello';
    type CardinalDirection = 'North' | 'East' | 'South' | 'West';
    ```

- 其他字面量类型

  - ```ts
    type OneToFive = 1 | 2 | 3 | 4 | 5;
    ```



### 用例：

```typescript
type Direction = keyof typeof Direction;
```

## readonly

TypeScript 类型系统允许你在一个接口里使用 `readonly` 来标记属性。它能让你以一种更安全的方式工作

- 函数参数上使用

  - ```typescript
    function foo(config: { readonly bar: number, readonly bas: number }) {
      // ..
    }
    ```

- 接口上使用

- type上使用   

### 泛型

- type    type Foo = Readonly<Foo>

- array   ReadonlyArray<number> 

  

### 其他示例

- ReactJS

## 与const的不同

```
const
```

- 用于变量；
- 变量不能重新赋值给其他任何事物。

```
readonly
```

- 用于属性；
- 用于别名，可以修改属性；



## 泛型

泛型常用 `T`、`U`、`V` 表示，如果有多个泛型，尽量语义话: **如 `TKey` 和 `TValue**`



## 类型推断

- 函数参数
- 返回值
- 结构
- 赋值

- noImplicitAny   这个选项表示当无法推断一个变量时发出一个错误（或者只能推断为一个隐式的 `any` 类型）



## Nerver

`never` 类型是 TypeScript 中的底层类型。它自然被分配的一些例子：

- 一个从来不会有返回值的函数（如：如果函数内含有 `while(true) {}`）；
- 一个总是会抛出错误的函数

### 与 `void` 的差异

当一个函数没有返回值时，它返回了一个 `void` 类型，但是，当一个函数根本就没有返回值时（或者总是抛出错误），它返回了一个 `never`



## 辨析联合类型

当类中含有[字面量成员](https://jkchao.github.io/typescript-book-chinese/typings/literals.html)时，我们可以用该类的属性来辨析联合类型。

```ts
type Shape = Square | Rectangle;
```

```ts
interface Square {
  kind: 'square';
  size: number;
}
```

```ts
function area(s: Shape) {
  if (s.kind === 'square') {
    return s.size * s.size;
  } else if (s.kind === 'rectangle') {
    return s.width * s.height;
  }

  // 如果你能让 TypeScript 给你一个错误，这是不是很棒？
    // const _exhaustiveCheck: never = s;
}
```

### strictNullChecks

### Redux 库正是使用的上述例子。

```ts
type Action =
  | {
      type: 'INCREMENT';
    }
  | {
      type: 'DECREMENT';
    };
store.dispatch({ type: 'INCREMENT' });
```



## 索引签名

```ts
const foo: {
  [index: string]: { message: string };
} = {};

// 储存的东西必须符合结构
// ok
foo['a'] = { message: 'some message' };
```

### 使用一组有限的字符串字面量

```ts
type Index = 'a' | 'b' | 'c';
type FromIndex = { [k in Index]?: number };
```

这通常与 `keyof/typeof` 一起使用，来获取变量的类型，在下一章节中，我们将解释它。

变量的规则一般可以延迟被推断：

```ts
type FromSomeIndex<K extends string> = { [key in K]: number };
```



## 流动的类型

当你改变了其中一个时，其他相关的会自动更新，并且当有事情变糟糕时，你会得到一个友好的提示，就好像一个被精心设计过的约束系统。

### [复制类型和值](https://jkchao.github.io/typescript-book-chinese/typings/movingTypes.html#%E5%A4%8D%E5%88%B6%E7%B1%BB%E5%9E%8B%E5%92%8C%E5%80%BC)

### 捕获变量的类型

```ts
let foo = 123;
let bar: typeof foo; 
```

### 捕获类成员的类型

```ts
class Foo {
  foo: number; // 我们想要捕获的类型
}

declare let _foo: Foo;

// 与之前做法相同
let bar: typeof _foo.foo;
```

### 捕获键的名称

```ts
const colors = {
  red: 'red',
  blue: 'blue'
};

type Colors = keyof typeof colors;
```



## 混合

起因：TS只能单继承

混合接受一个类，并且使用新功能扩展它。

```ts
type Constructor<T = {}> = new (...args: any[]) => T;
```











## Tips

- [export default` 被认为是有害的](<https://jkchao.github.io/typescript-book-chinese/tips/avoidExportDefault.html#export-default-%E8%A2%AB%E8%AE%A4%E4%B8%BA%E6%98%AF%E6%9C%89%E5%AE%B3%E7%9A%84>)

- Partial:

  - ```typescript
    type MyPartial<T> = {
      [P in keyof T]?: [T[P]];
    };
    ```

    

- DeepPartial

  - ```typescript
    type DeepPartial<T> = {
      [P in keyof T]?: T[P] extends Object ? DeepPartial<T[P]> : T[P];
    };
    ```

- [infer](<https://jkchao.github.io/typescript-book-chinese/tips/infer.html#%E4%BB%8B%E7%BB%8D>)

  推断出返回值类型

  ```ts
  type ReturnType<T> = T extends (...args: any[]) => infer P ? P : any;
  ```











