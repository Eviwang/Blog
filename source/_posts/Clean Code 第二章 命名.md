---
title: Clean Code - 命名
date: 2019-04-16 20:13:36
tags:
---

## 有意义的命名

### 2.1. 名副其实

- 名称应该已经答复了所有的大问题。写注释，就不是名副其实
- 注意命名，一旦发现更好的名称，就换掉旧的

### 2.3.避免误导

- 别用 accountList 来指定一组账号，除非真的是 List 类型。`accounts`都会好一些

- 同时存在`ProductInfo`与 `Product`这两个类。 但是他们理解起来其实没有区别。要区分名称，就要以读者能鉴别不同之处的方式来区分。

### 2.5. 使用读的出来的名称

错误例子：

- `genymd`
- `class DtaRcrd102`

### 2.6 使用可搜索的名字

- 找 `MAX_CLASSES_PER_STUDENT` 很容易，但找数字 7 就麻烦了
- e 也不是一个

### 2.7 避免使用编码

现代语言有丰富的类型，没必要加入如：
`phoneString`,后缀，前缀没有必要

### 2.8 避免思维映射

在作用域较小，也没有名称冲突时可能为 `i,j,k`。最好还是使用明确的意义。

### 2.9 类名应该是名词

### 2.10 方法名应当是动词或动词短语

- `postPayment,deletePage,save`
- `get,set,is`前缀
- 重载构造函数，使用描述参数的静态方法名
  ```
  Complex fulPoint = Complex.FromRealNumber(23.0)
  好于
  Complex fulPoint  = new Complex(23.0);
  ```

### 2.11 别扮可爱

### 2.12 每个概念对应一个词

给每个概念选一个词，并且一以贯之

- 项目中避免有时候用`fetch`、有时候用`get`、retrieve，给多个类中命名。
- 再比如：有时候用`xxManager`，有时候用`xxController`

### 2.13 别用双关语

如 ：`add`,使用`append,insert`会更加明确

### 2.14 使用解决方案领域名称。

比如 `AccountVisitor`,`JobQueue`

### 2.15 使用源自所涉问题领域名称。

### 2.16 添加有意义的语境

- `thereAreManyLetter,thereIsOneLetter`

### 2.17 不要添加有意义的语境
