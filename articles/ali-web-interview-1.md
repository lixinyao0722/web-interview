# 阿里前端社招面试题


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

| box-sizing属性值 | 类型      | 含义                         | 场景                                   |
|:----------------|:----------|:-----------------------------|:---------------------------------------|
| border-box      | IE盒模型  | width=content+padding+border | 表单多项padding、border不同时保证长度一致 |
| content-box     | 标准盒模型 | width=content width          | -                                      |


### flex弹性布局

- [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
- [Flex 布局示例](http://static.vgee.cn/static/index.html)

#### 相关概念

| 名称                                  | 含义                          |
|:--------------------------------------|:-----------------------------|
| [flex container](#flex-container属性) | 采用 Flex 布局的元素           |
| [flex item](#flex-item属性)           | 子元素                        |
| main axis                             | 默认水平方向，主轴             |
| cross axis                            | 默认垂直方向，交叉轴            |
| main start                            | 主轴的开始位置（与边框的交叉点） |
| main end                              | 主轴的结束位置                 |
| cross start                           | 交叉轴的开始位置               |
| cross end                             | 交叉轴的结束位置               |
| main size                             | flex item占据的主轴的空间      |
| cross size                            | cross item占据的主轴的空间     |

#### flex container属性

| 属性名           | 含义                                    | 可选值                                                                        | 默认值      |
|:----------------|:----------------------------------------|:-----------------------------------------------------------------------------|:-----------|
| flex-direction  | 设置主轴方向                             | row ; row-reverse ; column ; column-reverse                               | row        |
| flex-wrap       | 设置flex item换行方式                    | nowrap ; wrap ; wrap-reverse                                               | nowrap     |
| flex-flow       | flex-direction和flex-wrap属性的简写形式   | 见flex-direction和flex-wrap可选值                                             | row nowrap |
| justify-content | 定义flex item在主轴上的对齐方式           | flex-start ; flex-end ; center ; space-between ; space-around            | flex-start |
| align-items     | 定义flex item在交叉轴上的对齐方式          | flex-start ; flex-end ; center ; baseline ; stretch                      | stretch    |
| align-content   | 定义了多根主轴线的对齐方式，一根时该属性无效 | flex-start ; flex-end ; center ; space-between ; space-around ; stretch | stretch    |

#### flex item属性

| 属性名       | 含义                                                                        | 可选值                                                           | 默认值        |
|:------------|:----------------------------------------------------------------------------|:----------------------------------------------------------------|:-------------|
| order       | 定义item的排序顺序（小->大），可负数                                           | 整数                                                            | 0            |
| flex-grow   | container存在剩余空间时item的放大比例                                          | 非负整数                                                         | 0（不放大）   |
| flex-shrink | container空间不足时item的缩小比例                                             | 非负整数                                                         | 1（正常缩小） |
| flex-basis  | 定义在分配多余空间之前item占据的主轴空间。浏览器根据这个属性，计算主轴是否有多余空间 | {length} ; auto                                                | auto         |
| flex        | flex-grow, flex-shrink 和 flex-basis的简写                                   | 见flex-grow, flex-shrink 和 flex-basis属性可选值                 | 0 1 auto     |
| align-self  | 允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性                   | auto ; flex-start ; flex-end ; center ; baseline ; stretch | auto         |

### 未知宽高元素如何水平垂直居中

假定未知宽高元素为item，其父元素为container，对container做以下css样式控制。

```css
#container {
    background-color: #ffe665;
    height: 400px;
    display: flex;
    justify-content: center;
    align-items: center;
}
```

## JS部分

### 原型链、对象、构造函数之间的关系

- [完整原型链详细图解（构造实例对象.proto函数、原型、实例化对象）](https://blog.csdn.net/spicyboiledfish/article/details/71123162)

js原型链、对象及构造函数关系图如下， [点击下载](../assets/resources/process-on/js原型链图.pos) ProcessOn源文件。  
![js原型链图](../assets/imgs/js原型链图.png)

关键属性
1. 构造函数
2. 构造函数.prototype
3. 构造函数.prototype.constructor
4. `实例对象.__proto__` 

```javascript
构造函数 === 构造函数.prototype.constructor  

构造函数.prototype === 实例对象.__proto__  
```

### JS常见跨域手段。jsonp原理、cors如何设置

- [详解js跨域问题](https://segmentfault.com/a/1190000000718840)

#### cors方式 (cross origin resource share)

基本思想：利用自定义HTTP协议头让浏览器与服务器通讯，决定请求是否成功。

- 服务端设置

```
Access-Control-Allow-Origin: <origin> | *
```
`origin`被允许跨域访问这个资源的网站，* 代表全部网站。**浏览器会检测这个参数**，如果符合才会获取资源。

```
Access-Control-Allow-Credentials: true | false
```
是否允许浏览器请求资源时携带cookie信息。  
该属性要XMLHttpRequest设置`withCredentials = true`。

- 前端

```javascript
const xhr = new XMLHttpRequest()
xhr.open('GET', 'http://example.com/data.php') // 使用绝对路径
xhr.withCredentials = true // 浏览器请求时带上example.com域名cookie
xhr.onreadystatechange = (xhr, event) => {
  // 处理
}
xhr.send()
```

#### jsonp方式

原理：`XMLHttpRequest 1.0`无法请求不同域数据，但可以请求不同域script。jsonp需要前后端配合，代码样例如下。

- 前端部分

```html
<script type="text/javascript">
    function doSomething(json){
        //处理获得的json数据
        const obj = JSON.parse(json)
    }
</script>
<script src="http://example.com/data.php?callback=doSomething"></script>
```
- 后端部分

```php
$callback = urldecode(trim($_GET['callback']));
$data = [
        "ret" => 0,
        "msg" => "success",
        "data" => [
                "id" => 10000,
                "name" => "Tom",
                "age" => 20,
            ]
    ];
echo 'callback=(' . json_encode($data) . ')';
exit();
```
- 优点  
兼容性好，古老的浏览器同样适用

- 缺点  
只支持GET方式请求  
不能解决不同域的两个页面之间如何进行JavaScript调用的问题

#### document.domain方式

document.domain通过获得目标页面window完全读取权限方式进行通讯，前置条件如下。

- 可获取其他页面的window对象
- 两页面含有相同二级域名
- 协议相同
- 端口相同

常用场景，父页面与iframe引入的子页面进行通讯。  
假设父页面 `http://one.example.com/parent.html` 中有如下代码。

```html
<iframe id="iframe" src="http://two.example.com/child.html"></iframe> 

<script>
    document.domain = 'example.com'//提升域名
    const iframe = document.getElementById('iframe')
    const childDocument = iframe.contentDocument // 具有完全读写权限
    const childWindow = iframe.contentWindow // 具有完全读写权限
</script> 
```

子页面`http://two.example.com/child.html`

```html
<script>
    document.domain = 'example.com'//提升域名
</script>
```

#### window.name方式

原理：利用`window.name`不随url跳转而改变，与document.domain方式相比没有前置条件限制。出于安全原因，浏览器限制了`window.name`必须是字符串，常用场景如下。

假设父页面 `http://one.example.com/parent.html` 中有如下代码。

```html
<iframe id="iframe" src="http://any.other.com/child.html"></iframe> 

<script>
    const iframe = document.getElementById('iframe')
    iframe.onload = () => {
      iframe.onload = () => {
        //处理数据
        const data = iframe.contentWindow.name
      }
      //iframe获取了不同源的数据，再将其src指定同源页面，即可访问iframe.contentWindow对象，而iframe.contentWindow.name数据保持不变
      iframe.src = 'about:black'//about:blank，javascript: 和 data: 中的内容，继承了载入他们的页面的源
    }
</script>
```

子页面`http://any.other.com/child.html`只需要获取`any.other.com`域名数据并设置到`window.name`上即可。

#### window.postMessage方式

Html5新增API，其跨域能力不受同源限制，下面样例是iframe向父页面发送消息。

- 主页面

```javascript
// 监听消息事件
window.addEventListener('message', e => {
  // 只过滤需要的信息
  if (e.origin === 'http://one.example.com') {
    const {data} = e
    //处理数据
  } 
})

```

- 主页面引入的iframe页面

```javascript
const message = 'any'
const targetOrigin = '*'
// 通过window.parent对象向父页面发送数据
window.parent.postMessage(message, targetOrigin)
```

`iframe.contentWindow`: 接受消息的 Window 对象。  
`message`: 在最新的浏览器中可以是对象。  
`targetOrigin`: 目标的源，* 表示任意。


### 对象数组深度拷贝实现原理

- [javaScript中浅拷贝和深拷贝的实现](https://github.com/wengjq/Blog/issues/3)

#### js两种基本类型

- 值类型  
包括5种基本类型：Undefined、Null、Number、String、Boolean。变量和数据直接存放在栈内存中。

- 引用类型
包括对象、数组、函数等。变量保存是一个指向数据的指针，变量名存放于栈内存，数据存放于堆内存。

>1. 浅拷贝复制的是变量保存的指针，指向堆内存中同一片数据段，当修改数据时，两变量访问得到的值均发生改变。
>2. 深度拷贝会在堆内存中重新开辟一段内存，把源数据完整复制，复制变量指针指向新内存，修改数据时变量访问的值互不影响。

#### 深度拷贝实现方法

- 利用`JSON.parse`和`JSON.stringify`

```javascript
const obj = {name: 'Tom', age: 20}
const copyObj = JSON.parse(JSON.stringify(obj))
```

- 递归方式

1. 若数据为普通类型，直接赋值。
2. 若数据为对象或数组类型，递归复制。

### 如何获取一个元素到视图顶部的距离

### getBoundingClientRect获取的top和offsetTop获取的top区别

### 事件委托(事件代理)

#### 概念

1. 利用事件冒泡，把一个元素的响应事件委托到另一个元素上。
2. 一般场景把一个或一组元素的响应事件委托到外层元素。
3. 使用代理后需要自行处理事件派遣，即那种事件属于哪些代理元素。

#### 优点

1. 减少内存消耗，由于减少响应函数的创建次数。
2. 实现动态绑定事件。例如ul代理响应动态添加的li点击事件。

### XSS是什么，攻击原理，怎么预防

#### 概念

XSS全称跨站脚本攻击。

#### 攻击原理

利用网页没有过滤用户输入而直接输出到页面的漏洞。

#### 类型

- Dom Based XSS
>例如A站从url上取出参数username并输入到document中，则可以构造含脚本的特殊url进行攻击，任何点击的用户均受影响。

- Stored XSS
>例如博客网站，系统将用户的评论无过滤直接保存到db中，当其他用户浏览时又无过滤输出到document中，可构造含脚本的评论，任何浏览到该评论用户均受攻击。

#### 防御措施

检验用户输入，包括类型、值范围，对特殊字符进行转义。

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
