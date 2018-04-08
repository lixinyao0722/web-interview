# 阿里前端社招一


## CSS部分

### CSS盒模型

document中所有元素被表示为一个[盒子模型](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)，描述元素所占空间内容。每个盒子共有4边，从外到内分别如下。
>1. margin edge
>2. border edge
>3. padding edge
>4. content edge

标准盒模型height、width控制content，如下图。  
[![css-box-model](../assets/imgs/css-box-model.png)](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Box_Model/Introduction_to_the_CSS_box_model)

IE盒模型height、width包括content、padding、border，如下图。  
[![css-border-box-ie](../assets/imgs/css-border-box-ie.png)](https://www.jianshu.com/p/cc2bc404269b)


### box-sizing应用场景

[box-sizing的使用场景](https://www.jianshu.com/p/3375b15f568f)

| box-sizing属性值 | 类型      | 含义                         | 场景                        |
|:----------------|:----------|:-----------------------------|:----------------------------|
| border-box      | IE盒模型  | width=content+padding+border | 表单多项padding、border不同时保证长度一致 |
| content-box     | 标准盒模型 | width=content width          |                             |


### 弹性flex布局

### 未知宽高元素如何水平垂直居中


## JS部分

### 原型链、对象、构造函数之间的关系

## JS常见跨域手段。jsonp原理、cors如何设置

### 对象数组深度拷贝实现原理

### 如何获取一个元素到视图顶部的距离

### getBoundingClientRect获取的top和offsetTop获取的top区别

### 事件委托

### XSS是什么，攻击原理，怎么预防

### webpack实现原理与机制

### webpack配置entry多入口时配合CommonChunkPlugin时，代码如何切割

### webpack.optimze.UglifyJsPlugin压缩速度慢，如何提升

### webpack loader原理和机制，有没有写过

### babel插件transform-runtime和stage-2的作用

### babel将ES6转换ES5原理

### ES6箭头函数this问题，常见拓展运算符

### 对JS模块化规范CommonJs、UMD、CMD的理解，与ES6模块有何区别


## 网络协议

### http2.0、https、websocket特性

### http返回码200和304含义


## 算法

### 分查找的时间复杂度是多少，如何计算


## 数据结构

### 线性顺序存储结构和链式存储结构有什么区别？以及优缺点


## 持续集成

### git大型项目合作，如何持续集成


## 现场实战题

### 白板写代码，用最简洁的代码实现数组去重。


## 开放性试题

### 说一下以往项目用到的技术栈，有何难点，是如何解决的。

### 说一下以往项目可以改进的地方以及做的优秀的地方。


## 参考

- [面试分享：一年经验初探阿里巴巴前端社招](http://segmentfault.com/p/1210000010573211)
