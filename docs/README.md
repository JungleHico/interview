# 前端面试题



## HTML

### 块级元素和行内/内联元素

|          | 块级元素                                                     | 行内元素                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 特点     | 块级元素占据一行的空间                                       | 行内元素只占据内容的宽度                                     |
| 宽高     | 可以设置 `width` 和 `height`，`width` 默认 100%              | 设置 `width` 和 `height` 无效                                |
| 边距     | 可以设置 `margin` 和 `padding`                               | `margin` 和 `padding` 只能设置水平方向，不能设置垂直方向     |
| 常见标签 | `<div> <p> <h1> <form> <ol> <ul> <li> <audio> <video> <canvas>` | `<span> <a> <img> <button> <input> <label> <br> <i> <strong>` |



### HTML5 新特性

1. 新增语义化标签：`<header>`、`<footer>`、`<nav>`、`<aside>`、`<section>`、`<article>` 等。
2. 新增音频和视频标签：`<audio>` 和 `<video>`。
3. 本地化存储：`localStorage` 和 `sessionStorage`。
4. 支持 canvas。
5. 支持 web socket。
6. history API：`go`、`forward`、`back`、`pushstate`。



### src 和 href 的区别

`src` 和 `href` 都可以加载外部资源，区别在于：

- `src`：常用于 `<script>` 标签，会加载和解析资源，阻塞页面的渲染。
- `href`：常用于 `<link>` 和 `<a>` 标签，会并行下载资源，不会阻塞当前文档的加载。



### b 标签和 strong 标签的区别、i 标签和 em 标签的区别

- `<strong>` 是语义化标签，表示加重语气，而 `<b>` 标签只用于加粗效果，不过浏览器一般都会将 `<strong>` 的默认样式设为加粗。
- `<em>` 是语义化标签，表示强调语气，而 `<i>` 标签只用于斜体效果，不过浏览器一般都会将 `<em>` 的默认样式设置为斜体。



## CSS

### CSS 选择器及优先级

| 选择器         | 格式                 | 权重值 |
| -------------- | -------------------- | ------ |
| id 选择器      | `#id`                | 100    |
| 类名选择器     | `.classname`         | 10     |
| 属性选择器     | `input[type="text"]` | 10     |
| 伪类选择器     | `ul:first-child`     | 10     |
| 标签选择器     | `div`                | 1      |
| 伪元素选择器   | `a::after`           | 1      |
| 后代选择器     | `ul li`              | 0      |
| 子选择器       | `ul > li`            | 0      |
| 相邻兄弟选择器 | `label + input`      | 0      |
| 通配符选择器   | `*`                  | 0      |

注意：

- 权重值大的选择器优先级高；
- 内联样式的权重值为 1000；
- `!important` 的优先级最高；
- 如果优先级相同，则最后的样式生效。



### 常见的居中方式

1. `text-align: center` （文本水平居中）

2. `margin: 0 auto`（水平居中）
3. `line-height: 1em`（单行文本垂直居中）
4. 绝对定位：`position: absolute; top: 0; left: 0; transform: translate(-50%, -50%)`
5. 弹性布局：`display: flex; justify-content: center; align-items: center`



### 常见隐藏元素的方式

- `display: none`：元素会从文档树中删除，不会占据空间。
- `visibility: hidden`：元素仍然占据空间，但绑定的事件不生效。
- `opacity: 0`：元素的不透明度设为0，元素仍然占据空间且绑定的事件仍然生效。
- `position: absolute`：通过绝对定位，将元素设置到可视区域外。
- `z-index: -1`：通过其他元素将其盖住，来实现隐藏效果。



### transition 和 animation 的区别

- `transition`：用于定义 CSS 属性变化的效果，只涉及初始帧和结束帧，通常需要某个事件才能触发，例如点击（`:active`）、鼠标滑过（`:hover`）、聚焦（`:focus`）等。
- `animation`：可以更加灵活地定义动画，可以通过 `@keyframes` 定义多个动画帧，可以循环执行，不要事件就可以触发。



### 伪类和伪元素

- 伪类：用于设置元素在特定状态下的样式。常见的伪类有：`:hover`、`:active`、`:visited`、`:first-child` 等。

```css
a:hover {
  text-decoration: underline;
  color: blue;
}
```

- 伪元素：用于设置元素特定部分的内容和样式。常见的伪元素有：

| 伪元素           | 作用                               |
| ---------------- | ---------------------------------- |
| `::before`       | 在元素前面额外插入内容并设置样式   |
| `::after`        | 在元素后面额外插入内容并设置样式   |
| `::first-letter` | 设置块级元素第一行第一个字符的样式 |
| `::selection`    | 设置选中文本样式                   |



### 盒模型

盒模型由 `margin`、`border`、`padding` 和 `content` 四部分构成。

- 标准盒模型（默认）：`width` 和 `height` 范围只包含 `content`。

```css
div {
  box-sizing: content-box;
}
```

- IE盒模型（怪异盒模型）：`width` 和 `height` 的范围包含 `content`、`padding` 和 `border`。

```css
div {
  box-sizing: border-box;
}
```



### 分辨率、像素比和视口

- 物理分辨率：屏幕的实际分辨率，常见的有 1920\*1080、2560\*1440 等。
- 逻辑分辨率和设备像素比：随着移动设备的屏幕分辨率越来越高，如果1个像素点只渲染1个像素点对应的内容，那么图片和文字就会显得非常小，为了解决这个问题，浏览器的**逻辑分辨率**就诞生了。浏览器通过一个倍率降低分辨率，达到人眼能够看到的更好的效果。例如一台手机的**物理分辨率**是 1920\*1080，浏览器以**逻辑分辨率** 640\*320 来渲染页面，也就是3个物理像素点渲染1个像素的内容，这个比率被称为**设备像素比**。浏览器的**设备像素比**可以通过 `window.devicePixelRatio` 来获取。
- 视觉视口：指用户通过屏幕可以看到的区域，一般等于浏览器窗口大小。
- 布局视口：指页面布局的基准窗口，一般 PC 端浏览器的布局视口与浏览器窗口大小相等，但在移动端，布局视口有一个默认值，约为 `964px`（布局视口大小可以通过 `document.documentElement.clientWidth / clientHeight` 来获取），这样用户需要左右滚动和缩放才能看到页面的完整内容。为了解决上面的问题，我们通常通过 `<meta>` 标签设置浏览器的布局视口大小等于视觉视口的大小。

![viewport](./assets/viewport.awebp)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```



### 渐进增强和优雅降级

- 渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。



### CSS 性能优化

1. CSS 代码压缩；
2. 使用类名选择器代替标签选择器；
3. 避免使用通配符选择器（`*`）；
4. 后代选择器的层级不要超过三层；
5. 避免使用 `@import`；
6. 使用 `transition` 和 `animation` 代替 JS 实现简单的动画效果。



### 重排和重绘

- **重排**：当页面元素的尺寸、结构等发生变化时，浏览器会重写渲染部分或者整个文档，由于浏览器渲染页面是基于流式布局的，所以会导致周围的元素重新排列。常见的会引起重排的操作有：元素的尺寸、位置、内容、字体等发生变化，触发 CSS 伪类，添加或删除元素等。
- **重绘**：当元素的样式发生变化时，浏览器会对其重新绘制，但不会影响其他元素的位置。**重排一定会触发重绘，重绘时不一定会重排**。



### SCSS 和 Less 等 CSS 扩展语言有哪些特性

变量、嵌套、混合、导入等。



## JS

### DOM

**文档对象模型**（Document Object Model）是一个应用编程接口，网页可以抽象为一颗 DOM 树，开发者可以通过 DOM 树控制网页的内容和结构。

![DOM](./assets/dom.png)



### JS 基本数据类型和引用数据类型

- 基本数据类型：Boolean、Number、String、Undefined、Null、Symbol、BigInt
- 引用数据类型：Object（Function、Date、RegExp、Array、Map、Set...）



### undefined 和 null 区别

- undefined：变量未声明；变量声明但未初始化
- null：空对象指针；建议使用 null 初始化将来要保存对象的变量



### var、let  和 const 声明

1. `var` 声明的是函数作用域，`let` 声明的是块级作用域。

2. `var` 声明的变量会自动提升到函数作用域顶部，例如可以先使用后声明；而 `let` 声明的变量不会在作用域中被提升，即需要先声明再使用。
3. `const` 与 `let` 行为基本一致，只不过 `const` 声明的是常量，不允许被修改；如果 `const` 声明的变量是一个对象的引用，则对象内部可以被修改，只不过变量的引用不能修改。 



### 位操作符

| 符号  | 名称       | 操作                               |
| ----- | ---------- | ---------------------------------- |
| `&`   | 与         | 两位都是1时返回1，否则为0          |
| `|`   | 或         | 有一位是1时返回1，两位都是0时返回0 |
| `~`   | 非         | 取反操作，最终数值取反减1          |
| `^`   | 异或       | 相同为0，不同为1                   |
| `<<`  | 左移       | 所有数值左移，低位补0，保留符号位  |
| `>>`  | 有符号右移 | 所有数值右移，高位用符号位补充     |
| `>>>` | 无符号右移 | 所有数位右移，高位补0              |



### == 操作符的判断及强制类型转换规则

若两个操作数类型相同，则比较值是否相等；若两者类型不同，则会进行**强制类型转换**：

1. 如果两者分别是 `null` 和 `undefined`，则返回 `true`；
2. 如果其中一个操作数是 `boolean` 类型，则转化为 `number`（`true` 转化为 `1`，`false` 转化为 `0`）；
3. 如果其中一个操作数是 `string` 类型，另一个是 `number` 类型，则会调用 `Number()` 方法将 `string` 转化为 `number`（如果包含非数字字符，则转化为 `NaN`，如果为空字符串，则转化为 `0`）；
4. 如果其中一个操作数是 `object`，另一个是基本数据类型，则调用对象的 `valueOf()` 转化为基本数据类型；
5. 如果两个操作数都是 `object`，则比较引用的是否为同一个对象；
6. 如果任意一个操作符是 `NaN`，则返回 `false`（`NaN` 和 `NaN` 不相等）。



### == 和 ===

`==` （不全等）不保证两个操作数的类型和值都相等，只表示类型转换后的值相等。

`===` （全等）表示两个操作数的类型和值都相等。



### 如何令 a == 1 && a == 2 && a == 3 成立

- 重写对象的 `valueOf()` 方法：使用 `==` 比较时，如果一个操作数是对象，另一个操作数是基本类型，就会调用对象的 `valueOf()` 方法。

```js
const a = {
  i: 1,
  valueOf() {
    return this.i++;
  },
};
```

- 使用 `Object.defineProperty()` 在当前上下文定义 `a` 属性，并修改 `get()` 函数：

```js
let _a = 1;
Object.defineProperty(this, 'a', {
  get() {
    return _a++;
  },
});
```



### 箭头函数和普通函数

箭头函数相比于普通函数，有以下特点：

1. 不能作为构造函数
2. 不能使用 `arguments` 对象，需要使用剩余参数代替
3. 普通函数 `this` 指向调用函数的上下文（谁调用了函数，`this` 就指向谁），是可变的；箭头函数的 `this` 指向函数定义时的上下文，是固定的



### this 的指向

- 普通函数的 `this` 指向调用函数的上下文对象，也就是谁调用这个函数， `this` 就指向谁，如果直接调用，则指向全局对象，这个值只有在函数执行时才能确定。
- 可以通过函数的 `apply()`、`call()` 和 `bind()` 方法改变函数 `this` 的指向。



### forEach() 方法可以退出循环吗？

除抛出异常之外，没有其他方法可以停止或中断循环（`continue/break` 无效，`return` 等同于 `break`）。当你需要通过抛出异常来退出循环时，说明该场景不适合使用 `forEach()` 。



### 闭包

闭包指的是**引用了另一个函数作用域中变量的函数**，通常是在嵌套函数中，当内部函数引用了外部函数的变量，即使外部函数执行完，作用域链被销毁，内部函数还是保留其活动对象，这些变量仍然保留在内存中，这就造成了内存泄漏，采用引用计数垃圾回收机制的旧浏览器就无法进行垃圾回收。



### 闭包的作用

1. 创建私有变量
2. 使函数中的变量继续保存在内存中



### 执行上下文

当执行一个函数时，我们称进入了一个执行上下文（或者叫执行环境），JS 通过执行上下文栈来管理上下文，可以分为三个阶段：

1. **创建阶段**：当调用函数时，会为该函数创建一个执行上下文并压入栈中。JS 一开始在全局环境执行时会创建全局上下文并压入栈中。
2. **执行阶段**：JS 会先执行上下文栈顶的函数。
3. **回收阶段**：当函数执行完后，会从上下文栈中弹出并执行下一个函数，该函数作用域中创建的变量也会等待垃圾回收。当所有代码执行完后，全局上下文也会弹出。



### 变量对象和作用域链

- **变量对象**：每个执行上下文都会有一个变量对象，用于保存当前上下文定义的变量和函数（一开始会添加通过函数声明定义的函数以及通过 `var` 声明的变量 ）。
- **作用域链**：当执行上下文代码时，JS 会创建一个作用域链，用于决定上下文访问变量和函数的顺序。当前上下文的变量对象始终处于作用域链的最顶端，同时作用域链还会包含上一个上下文的变量对象，以此类推，直至全局上下文。当解析变量时，会通过变量的标识符从作用域链中进行查找，首先会从当前上下文的变量对象中查找，如果没有找到，会沿着作用域链往上一级上下文的变量对象里边查找，以此类推。由此可以看出，内部上下文可以通过作用域链访问外部上下文的变量，反之则不行；除此之外，内部上下文可以替换外部上下文中的同名变量。



### 函数防抖和函数节流

函数防抖（debounce）和函数节流（throttle）通过控制函数一定时间内的执行次数，来避免某些函数频繁执行带来的性能损耗，常用于限制事件监听，如输入框联想，滚动监听等。

- 防抖：函数必须间隔特定时间才能执行，如果期间重复触发，就会重新计时
- 节流：一定时间内，只会执行一次函数

```js
// 防抖
function debounce(func, wait = 0) {
  let timer = null;
  return function () {
    if (!timer) {
      timer = setTimeout(function () {
        func.apply(this, arguments);
        timer = null;
      }, wait);
    }
  };
}

// 节流
function throttle(func, wait = 0) {
  let timer = null;
  return function () {
    if (!timer) {
      func.apply(this, arguments);
      timer = setTimeout(() => {
        timer = null;
      }, wait);
    }
  };
}
```



### 栈内存和堆内存

- **栈内存空间**：用栈作为数据结构在内存中所申请的空间。基本数据类型变量存储在栈内存中，因为基本数据类型占用空间小、大小固定，通过值来访问，属于被频繁使用的数据。
- **堆内存空间**：用堆作为数据结构在内存中所申请的空间。引用数据类型存储在堆内存中，引用数据类型占据空间大、大小不固定，如果存储在栈中，将影响程序的运行性能。引用数据类型会在栈中存储一个指针，这个指针指向堆内存空间中该实体的起始地址。



### JS 垃圾回收机制

JavaScript 垃圾回收程序每隔一个周期，就会判断哪些变量不再使用，然后释放它占用的内存。JS 垃圾回收机制一般分为两种：

- **标记清理**（mark-and-sweep）（常用）：当变量进入上下文，比如在函数内部声明一个变量时，这个变量就会被标记为存在上下文中；当变量离开上下文，例如函数执行完，该变量就会被标记为离开上下文，这样，下一次垃圾回收程序清理内存时，就会释放该变量的内存。
- **引用计数**（reference counting）（旧版本浏览器）：当一个值被一个变量引用时，该值的引用数加 1，当引用该值的变量被其他值覆盖时，该值的引用数减 1，当引用数为 0 时，说明该值不需要被用得到，则内存可以被回收。这种回收机制有个弊端，当两个对象通过属性值**循环引用**时，它们的引用数都是 2，即使函数执行完，这两个对象不在作用域中时，这两个变量也不会被垃圾回收程序释放。



### 哪些情况会导致内存泄漏

- **意外的全局变量：** 由于使用未声明的变量，而意外的创建了一个全局变量，而使这个变量一直留在内存中无法被回收。

- **被遗忘的计时器或回调函数：** 设置了 setInterval 定时器，而忘记取消它，如果循环函数有对外部变量的引用的话，那么这个变量会被一直留在内存中，而无法被回收。

- **脱离 DOM 的引用：** 获取一个 DOM 元素的引用，而后面这个元素被删除，由于一直保留了对这个元素的引用，所以它也无法被回收。

- **闭包：** 不合理的使用闭包，从而导致某些变量一直被留在内存当中。



### 深拷贝和浅拷贝

- **浅拷贝**：只复制引用地址，新旧对象共享相同的内存空间，修改新对象属性会影响原对象，常见的浅拷贝方法：扩展运算符、`Object.assign`、`Object.create`、`Array.protorype.slice` 和 `Array.prototype.concat`
- **深拷贝**：创建一个于原对象一模一样的新对象，新旧对象不共享内存空间，修改新对象属性不会影响原对象，常见的深拷贝方法：`lodash.cloneDeep`、`JSON.stringify` 以及手写递归方法

其中，使用 `JSON.stringify` 进行深拷贝的弊端：

1. 不支持 undefined、symbol 和函数类型
2. Date 类型会转化为字符串
3. 只能序列化可枚举的属性



### Map 和 WeakMap 区别

- Map 的 key 可以是任意数据类型，WeakMap 的 key 必须是对象。
- Map 的 key 如果是对象，就相当于这个对象被引用，就不会被当做垃圾回收；WeakMap 的 key 不属于正式引用，不会阻止垃圾回收，也就是说，如果 key 没有其他引用，就会执行垃圾回收。
- 因为 WeakMap 中的 key/value 任何时候都有可能被销毁，所以 WeakMap 本身不可迭代。 



### 原型对象、原型链



### 原型链的终点

`Object` 是其他对象的基类，所以所有对象的原型链最终都会指向 `Object` ，而 `Object` 的原型对象是 `null`。



### JS 设计模式

#### 工厂模式

工厂模式用于创建多个类似的对象，但是创建的对象不属于同一个类型（除了 `Object`）

```js
function createPerson(name, age) {
  let obj = new Object();
  obj.name = name;
  obj.age = age;
  obj.sayName = function () {
    console.log(this.name);
  };
  return obj;
}

const person = createPerson('Tom', 18);
person.sayName(); // Tom
```



#### 构造函数模式

构造函数模式解决了创建特定类型对象的问题，但是构造函数定义的方法，在每个实例上都会被创建一遍。

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
  this.sayName = function () {
    console.log(this.name);
  };
}

const person = new Person('Tom', 18);
person.sayName(); // Tom
console.log(person instanceof Person); // true
```



#### 原型模式

通过原型模式创建的属性和方法，所有实例都可以通过原型链查找访问到，也就是说是共享的。原型模式不能在创建实例时传递参数，除此之外，由于原型对象共享属性和方法，修改引用类型的原型属性时，会出现数据污染的问题。

```js
function Person() {}

Person.prototype.name = 'Tom';
Person.prototype.age = 18;
Person.prototype.sayName = function () {
  console.log(this.name);
};

const person = new Person();
person.sayName(); // Tom
console.log(Object.getPrototypeOf(person) === Person.prototype); // true
```



#### 组合模式

组合模式通过构造函数模式定义实例属性，通过原型模式定义共享属性和方法，既可以通过构造函数传参，又可以通过原型共享节省内容。

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.sayName = function () {
  console.log(this.name);
};

const person = new Person('Tom', 18);
person.sayName(); // Tom
console.log(person instanceof Person); // true
console.log(Object.getPrototypeOf(person) === Person.prototype); // true
```



#### 类

ES6 引入 `class` ，本质上是组合模式的语法糖。

```js
class Person {
  constructor(name, age) {
    this.name = name;
    this.age = age;
  }

  sayName() {
    console.log(this.name);
  }
}

const person = new Person('Tom', 18);
person.sayName(); // Tom
console.log(person instanceof Person); // true
```





### 通过 new 创建实例的过程

1. 在内存中创建新对象。
2. 新对象的原型指针指向构造函数的原型。
3. 构造函数内的 `this` 指向新对象。
4. 执行构造函数内部代码。
5. 如果构造函数返回非空对象，则返回该对象，否则返回刚创建的新对象。



### 如何判断一个对象是某个类的实例

1. `instanceof`
2. 判断对象的 `constructor` 属性是否为类的构造函数
3. 判断对象的原型指针是否指向类的原型

```js
console.log(person instanceof Person);
console.log(person.constructor === Person);
console.log(Object.getPrototypeOf(person) === Person.prototype);
```



###  遍历对象属性的方法

- `for-in`：遍历实例及其原型对象的所有可枚举属性。
- `Object.keys()`：只返回实例本身的可枚举属性。
- `Object.getOwnPropertyNames()`：返回实例及其原型对象的所有属性，包含不可枚举的（例如 `constructor`）。



### Proxy

代理（Proxy）是 ES6 新增的特性，可以对对象的读写等操作进行拦截：

```js
const target = {
  name: 'target',
};

const handler = {
  get(target, key) {
    console.log(`属性${key}被读取，值为：${target[key]}`);
    return target[key];
  },
  set(target, key, value) {
    console.log(`属性${key}被设置，旧值为：${target[key]}，新值为：${value}`);
    target[key] = value;
    return value;
  },
};

const proxy = new Proxy(target, handler);

console.log(proxy.name);
proxy.name = 'target2';
console.log(proxy.name);
```

Proxy 的应用场景：隐藏属性、数据验证、函数参数验证、数据绑定（Vue）。



### Promise、async/await

- `Promise` 是 ES6 增加的一种异步编程机制，可以解决“回调地狱”的问题。

- `async/await` 是 ES2017 推出的 `Promise` 的语法糖，可以使用更加接近同步编程的方式处理异步代码。使用 `async` 声明的函数叫做异步函数，异步函数的返回值会被 `Promise.resolve` 包装成一个 `Promise` 对象。`await` 需要在异步函数中使用，`await` 可以暂停异步函数代码的执行，等待异步代码执行完，再执行其他代码。



### Promise.all、Promise.race、Promise.any

- `Promise.all()`：所有 `Promise` 都解决则返回一个解决值得数组，如果有 `Promise` 拒绝，则会返回第一个拒绝的状态值。
- `Promise.race()`：会返回第一个解决或者拒绝的 `Promise`，这个方法也称为竞速方法。
- `Promise.any()`：会返回第一个解决的 `Promise` 的结果，如果全部拒绝则返回失败结果。



### JS 单线程

- **进程**：资源分配的最小单位
- **线程**：CPU 调度的最小单位

进程是火车，线程是车厢，线程在进程下运行，一个线程无法独立运行，一个进程可以包含多个线程（一辆火车可以有多个车厢）。进程要比线程消耗更多的计算机资源（加列火车比加节车厢更耗资源）。

- JS 是单线程语言，执行完一个任务之后才能执行其他任务。
- 浏览器内核是多线程。一些 I/O 操作、定时器和事件监听都是由浏览器提供的其它线程来完成的。



### JS 事件循环和任务队列

JS 是单线程语言，事件循环是 JS 的执行机制，可以处理同步任务和异步任务。

在一次事件循环中，遇到同步任务，立即执行，遇到异步任务，将其放到任务队列中，同步代码执行完之后，检查当前任务队列中是否有异步任务，如果有，则执行异步任务；如果没有，则继续执行同步任务。



### 宏任务和微任务

**宏任务**：script、计时器、网络请求、事件、文件读写

**微任务**：Promise

异步任务可分为宏任务和微任务，这两者主要是执行顺序不同，每次执行完宏任务之后，先执行微任务队列里边的微任务，然后再执行下一个宏任务。

一道经典面试题，写出以下代码的输出顺序：

```js
console.log(1);

setTimeout(() => {
  console.log(2);
}, 0);

new Promise((resolve, reject) => {
  console.log(3);
  resolve();
  console.log(4);
}).then(() => {
  console.log(5);
});

console.log(6);

// 1 3 4 6 5 2
```

首先，打印 1 是同步代码，直接执行；

然后定时器是宏任务，放到宏任务队列中；

然后 `Promise` 构造函数本身是同步代码，因此按顺序打印 3 和 4；

然后 `Promise` 的 `then` 毁掉函数是微任务，放到微任务队列中；

打印 6 是同步代码直接执行；

当前宏任务执行完毕（script 本身就是一个宏任务），执行所有微任务，打印 5；

执行下一个宏任务，打印 2。



### GET 请求和 POST 请求

|          | GET 请求                                    | POST 请求                                        |
| -------- | ------------------------------------------- | ------------------------------------------------ |
| 发送方式 | 通过 URL 发送，参数通过 & 连接              | 发送请求体                                       |
| 数据类型 | 只支持 ASCII 字符                           | 二进制数据                                       |
| 语义     | 用于请求数据                                | 用于提交数据                                     |
| 缓存     | 能被浏览器缓存，再次访问返回304             | 不能被浏览器缓存                                 |
| 数据长度 | 浏览器对 URL 长度有限制，一般是 2048 个字符 | 无限制                                           |
| 数据包   | 一次发送                                    | 浏览器一般分两次发送，先发送请求头，再发送请求体 |
| 安全     | 敏感数据放在 URL 请求参数中会暴露           |                                                  |



### 如何解决跨域问题

1. JSONP

JSONP（JSON with padding）是通过动态创建`<script>` 元素并为 `src` 属性指定跨域 URL 实现的。JSONP 可以从不同域拉去可执行代码，但不能防止域的恶意代码，而且不能确定 JSONP 请求是否失败。

2. CORS

CORS（Cross-Origin Resource Sharing）跨域资源请求，通过使用自定义 HTTP 头部来实现浏览器与服务器的跨域通讯，服务器端通过 `Access-Control-Allow-Origin` 匹配浏览器请求。

3. proxy

受浏览器同源策略的影响，浏览器不能跨域访问接口，而服务器不受此策略的影响，所以可以通过本地服务器代理请求，然后访问不同源的接口。



### cookie 和 Storage

|           | cookie                           | Storage                                                      |
| --------- | -------------------------------- | ------------------------------------------------------------ |
| http 请求 | 发送请求时请求头会包含 cookie    | Storage 只存储在客户端                                       |
| 大小      | 一般4KB                          | 一般5MB                                                      |
| 有效期    | 可以设置过期时间，默认浏览器关闭 | `localStorage` 长期保存，`sessionStorage` 持续到网页会话被关闭 |



### JS 模块化的发展

1. 引入多个 script 文件，需要手动管理文件加载顺序，而且无法避免变量污染的问题
2. 通过立即执行函数对代码进行封装
3. Node 使用 CommonJS 规范来封装模块
4. ES6 原生支持模块的导入导出



### ES6 新特性（总）

1. 新增块级作用域及 `let` 和 `const` 声明
2. 解构赋值
3. 扩展运算符
4. 新增数据结构：`Map`、`Set`、`WeakMap` 和 `WeakSet`
5. 新增数据类型 `symbol`
6. `Promise`
7. `Proxy` 和 `Reflect`
8. 类
9. 模块化



## TypeScript

### 什么是 TypeScript

TypeScript 是一个强类型的 JavaScript 超集，支持 ES6 语法，支持面向对象编程的概念，如类、接口、继承、泛型等。TypeScript 并不直接在浏览器上运行，需要编译器编译成纯 Javascript 来运行。



### TS 中 any 的作用

为编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，比如来自用户输入或第三方代码库。 这种情况下，我们不希望类型检查器对这些值进行检查而是直接让它们通过编译阶段的检查。



### TS 中接口和类型别名有什么异同点

#### 相同点

1. 都可以描述对象和函数

```typescript
interface Person {
  name: string;
  age: number;
}
```

```typescript
type Person = {
  name: string;
  age: number;
};
```

2. 都可以被继承

```typescript
interface Person {
  name: string;
  age: number;
}

interface Student extends Person {
  grade: number;
}
```

```typescript
type Person = {
  name: string;
  age: number;
};

// 交叉类型
type Student = Person & {
  grade: number;
};
```

#### 不同点

1. 除了对象和函数，`type` 还可以指定基本类型、联合类型、元组等。

```typescript
type Name = string;
type Account = string | number;
```

2. `interface` 可以重复声明，等同于两个接口进行合并。

```typescript
interface Person {
  name: string;
}

interface Person {
  age: number;
}

const person: Person = {
  name: 'Tom',
  age: 18,
};
```



### TS 中 typeof 和 keyof

- `typeof`：TS 中 `typeof` 可以获取变量的声明或者对象的类型。
- `keyof`：`keyof` 可以获取某种类型的所有键，返回值是联合类型。

```typescript
interface Person {
  name: string;
  age: number;
}

const person: Person = { name: 'Tom', age: 18 };

type TypeOfPerson = typeof person; // Person
```

```typescript
interface Person {
  name: string;
  age: number;
}

type KeyOfPerson = keyof Person; // "name" | "number"
```



### TS 泛型

泛型是指在定义函数、接口或类的时候，不指定具体的类型，而是可以和不同类型一起工作，从而实现复用。

```typescript
function getValue<T>(value: T): T {
  return value;
}

const num = getValue<number>(1);
const str = getValue<string>('a');
```



### TS 模块加载机制

1. 首先，编译器会尝试定位需要导入的模块文件，通过绝对或者相对的路径查找方式；
2. 如果没有查找到对应的模块，编译器会尝试定位一个类型声明文件（`*.d.ts`）；
3. 最后，如果编译器还是不能解析这个模块，则会抛出一个错误。

> `tsconfig.json` 配置文件中，可以通过 `files`、`include` 和 `exclude` 指定编译的文件（`*.ts`和 `*.d.ts`）。



### TS 中 declare 用法

在 TS 的类型声明文件中，通过 `declare` 声明一些全局变量、全局方法、全局对象等。其中，`declare global` 可以扩展全局变量的类型。



## Vue

### MVVM 

M（`Model`），即数据模型；V（`View`），即视图。

传统的开发模式，例如原生 JS 或者 jQuery，视图和模型是不分离的，更新数据时需要先找到视图，即需要更新数据的元素，这种方式当业务逻辑变得复杂之后就会难以维护。

MVVM 实现了模型和视图的分离，通过 MV（`ViewModel`），将数据与视图绑定，更新数据时会自动更新视图，视图变化时也会通知 ViewModel 更新数据。



### Vue 3 响应式数据的基本实现

Vue 2 中使用 `Object.defineProperty()` 来实现对对象属性的读取和设置，Vue 3 中采用 ES6 的 [Proxy](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 语法。**Proxy 是一个对象，它包装了另一个对象，并允许你拦截对该对象的任何交互。** 通过 Proxy 对数据的读取和设置进行拦截，当读对象的属性时，触发 `get` 函数，将副作用函数存入集合中；当设置对象的属性时，触发 `set` 函数，从集合中取出副作用函数并执行，这样就实现了简单的响应式数据。



### Vue3 新特性

1. 引入组合式 API，使业务逻辑关注点更加集中，提高代码复用性和可维护性。
2. 更好的 TS 支持。
3. 新增 `<Teleport>` 组件，可以将插槽内容渲染到指定外层 DOM。
4. Fragments，支持多根节点，减少节点层数，提高渲染性能。
5. 重构响应式系统，使用 `Proxy` 代替 Vue 2 的 `Object.defineProperty` 实现响应式数据。
6. 新增静态标记（patchFlag）（编译器），提高渲染效率（渲染器）。



### 为什么 data 选项需要通过一个函数返回一个对象？

如果 `data` 直接指定一个对象，那么多个组件就会引用同一个数据，一个组件修改数据会污染其他组件的数据。通过一个函数返回数据对象，可以通过函数作用域进行隔离。



### v-if 和 v-show

`v-if` 是**真实**的条件渲染，是**惰性**的，只有当表达式的值为 `true` 时才会被渲染，当表达式的值为 `false` 时不会渲染，并且会销毁原有的元素。

`v-show` 元素始终会被渲染，只是通过 CSS 的 `display` 属性控制元素的显示与隐藏。

`v-if` 具有更高的切换开销，而 `v-show` 具有更高的初始化渲染开销。



### 为什么不推荐同时使用 v-for 和 v-if（v-for 和 v-if 优先级）

- Vue 2 中 `v-for` 的优先级比 `v-if` 高，`v-if` 会重复运行在每个 `v-for` 循环中，如果想要有条件的跳过循环，则可以将 `v-if` 至于外层；
- Vue 3 中 `v-if` 的优先级比 `v-for` 高，这意味着 `v-if` 无法访问 `v-for` 的作用域内的变量。



### 为什么推荐为 v-for 提供 key

Vue 默认按照“就地更新”的策略来更新通过 `v-for` 渲染的元素列表。当数据项的顺序改变时，Vue 不会随之移动 DOM 元素的顺序，而是就地更新每个元素，确保它们在原本指定的索引位置上渲染。

默认模式是高效的，但**只适用于列表渲染输出的结果不依赖子组件状态或者临时 DOM 状态 (例如表单输入值) 的情况**。

为每个元素指定唯一的 `key` 属性，Vue 执行 Diff 算法更新节点时，就可以根据标识重用和重新排列现有元素。



### 为什么 Vue 3 的 setup 函数中不能使用 this？

因为 `setup` 函数在组件创建之前执行，所以 `setup` 函数中的 `this` 并不是组件实例的引用，因此应当避免在 `setup` 函数中使用 `this`。



### 如何理解 Vue 的单向数据流

所有的 props 都遵循着**单向绑定**原则，props 因父组件的更新而变化，自然地将新的状态向下流往子组件，而不会逆向传递。这避免了子组件意外修改父组件的状态的情况，不然应用的数据流将很容易变得混乱而难以理解。



### computed 和 watch

1. `computed` **支持缓存**，只在相关响应式依赖发生改变时，才会重新求值；`watch` **不支持缓存**，只要数据发生变化，就会执行侦听函数。
2. `computed` 的职责仅为计算和返回值，不应该有其他副作用（**异步请求或更改 DOM**）；`watch` 相对更加通用，**适合执行异步或者开销较大的操作**。



### vue 组件传参方法

1. 父组件通过 `props` 传数据给子组件
2. 子组件通过 `emit` 自定义事件传递数据
3. 祖先组件通过 `provide` 传递数据，后代组件通过 `inject` 接受数据
4. 父组件通过 `refs` 获取子组件实例
5. Vue 2 eventBus
6. 状态管理 Vuex/Pinia



### Vue 3 中代码复用的方式

1. **组件**：构建模块和 HTML 代码的复用
2. **组合式函数**：逻辑（JS 代码）的复用，例如把某个业务封装到 `useXXX()` 函数中然后导出。
3. **自定义指令**：复用 HTML 元素的 DOM 操作，比如元素自动聚焦、图片懒加载。



### Vue 3 内置组件

- Transition、TransitonGroup
- KeepAlive
- `Teleport`



### keepAlive

`<keep-alive>` 是 Vue 的一个内置组件，可以缓存组件，当组件切换时不会被销毁。

- `<keep-alive>` 默认会缓存所有组件，可以通过 `include/exclude` 控制要缓存的组件。
- 可以通过 `onActivated()` 和 `onDeactivated` 生命周期监听组件的显示/隐藏。



### vue-router history 模式和 hash 模式

|            | hash 模式                                                    | history 模式                                                 |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| url        | 包含哈希符号 `#`                                             | 不包含 `#`                                                   |
| 无刷新实现 | 通过 `window.onhashchange` 来监听 `hash` 的变化，借此实现无刷新跳转 | 通过 `history.pushState` 和 `history.replaceState` 来实现无刷新跳转 |
| 服务器配置 | 不需要服务器层面做处理                                       | 服务器需要配置回退路由，否则会出现刷新页面404的问题          |
| SEO        | `hash` 模式的页面跳转都在客户端中，不利于 SEO                | SEO 友好                                                     |



### Vue 路由守卫

- 全局路由守卫：`beforeEach`、`beforerResolve`、`AfterEach`
- 路由独享守卫：`beforeEnter`
- 组件内守卫：`beforeRouteEnter`、`beforeRouteUpdate`、`beforeRouteLeave`



### Vue 源码解析

[JungleHico/vue-source: Vue3 源码解析与实现，包含响应系统、渲染器和组件化 (github.com)](https://github.com/JungleHico/vue-source)



## Node.js

### 什么是 Node.js？

Node.js 是基于 Chrome V8 引擎的 JavaScript 运行环境，它可以用于搭建服务端。



### Node 解决了哪些问题

Node 在处理高并发、I/O 密集型场景有明显的性能优势

- 高并发：同一时间并发请求服务器
- I/O 密集型：指文件操作、网络请求、数据库访问



### Node 事件循环

进程启动时，Node 会创建一个循环，每次循环（Tick）时会查看是否有事件需要处理，如果有就取出事件并执行其回调函数，然后进入下一次循环，如果没有事件，则退出进程。



## 前端工程化

### Webpack

[[JungleHico/webpack-doc: webpack 使用文档 (github.com)](https://github.com/JungleHico/webpack-doc)]([JungleHico/webpack-doc: webpack 使用文档 (github.com)](https://github.com/JungleHico/webpack-doc))



### Webpack 打包过程

1. 初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数。
2. 开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译。
3. 确定入口：根据配置中的 entry 找出所有的入口文件。
4. 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理。
5. 完成模块编译：在经过第 4 步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系。
6. 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会。
7. 输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。



### Webpack Loader 和 Plugin

|          | Loader                                                       | Plugin                                                       |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 作用     | webpack 默认只支持编译 js 模块，而通过 loader，webpack 可以支持各种语言和预处理器编写模块。 | plugin 可以以扩展 webpack 的功能，让 webpack 具有更多的灵活性。 |
| 加载顺序 | 从后往前                                                     | 从前往后                                                     |



### 开发环境和生产环境

开发环境（`development`）和生产环境（`production`）的构建目标差异很大。

- 在开发环境中，我们需要具有强大的、具有实时重新加载（live reloading）或热模块替换（hot module replacement）能力的 source map 和 localhost server。
- 在生产环境中，我们的目标则转向于关注更小的 bundle，更轻量的 source map，以及更优化的资源，以改善加载时间。



### source-map

当 webpack 打包源代码时，可能会很难追踪到错误和警告在源代码中的原始位置。为了更容易地追踪错误和警告，JavaScript 提供了 source map 功能，将编译后的代码映射回原始源代码。webpack 通过 `devtool` 属性来配置不同的 `source-map` 值。使用不同的 `source-map` 值，代码的构建速度和代码映射是不一样的。

- 对于开发环境，通常希望以增加编译后包的体积为代价，获取编译较快速且调试友好的 source map。
- 但是对于生产环境，则希望分离和压缩模块，获得体积较小且不能有原始源代码（可以有行列信息供调试）的 source map。



### Webpack 构建优化

1. 对于生产环境，可以通过 `webpack-bundle-analyzer` 插件将打包后的结果以矩形树图的方式进行可视化显示，方便我们进行模块分析和性能优化。
2. 通过设置 `source-map` 的值，使开发环境的打包速度更快，生产环境的打包体积更小。
3. 通过 `thread-loader`，利用多线程进行打包。
4. 通过 `externals` 属性，以外部扩展的形式引入代码库，这样就可以通过 CDN 进行加速了。 
5. Tree-Shaking，webpack 自带，可以剔除不需要用到的代码。



### 浏览器缓存和代码分离



### 权限控制

路由权限（菜单权限）、接口权限、动作权限



### 浏览器缓存

浏览器缓存策略分为**强缓存**和**协商缓存**两种。

#### 强缓存

强缓存不会向服务器发请求，而是从缓存中读取资源，强缓存可以通过 response header 的 `expires` 和 `cache-control` 进行控制。

`expires` 表示缓存的过期时间，有个缺点是受本地时间影响，修改本地时间会影响缓存。

`cache-control` 的优先级比 `expires` 高，有多个取值，最常见的是 `max-age`，表示缓存的有效时间，比如 `cache-control: max-age=600` 表示 600 秒后过期。

#### 协商缓存

协商缓存就是强制缓存失效后，浏览器携带缓存标识向服务器发起请求，由服务器根据缓存标识决定是否使用缓存的过程。协商缓存可以通过 response header 的 `last-Modifined` 和 `etag` 进行控制。

`last-modifined` 表示文件最后修改时间，当浏览器第二次请求资源时，请求头会添加这个过期时间，服务器会将这个时间和文件最后修改时间比较，如果没有变化，说明资源没有变化，于是返回 304 状态码；如果资源有变化，则返回新的资源，状态码为 200。

`etag` 与 `last-modefined`  类似，只不过是一个 `token`，发送请求时比较本地 `token` 与服务器 `token` 是否一致。`etag` 的优先级比 `last-Modefined` 高。



## 性能优化

### 为什么通常把  `<script>` 标签放在 `<body>` 页面元素的后面而不是 `<head>` 标签中？

把 JS 文件放在 `<head>` 里，则页面渲染需要等到 JS 文件下载、解析后，期间页面会呈现空白，也就是会阻塞页面的选阿然。



### CDN



### 图片懒加载



## 计算机网络

### 在地址栏里输入一个地址回车会发生哪些事情？

1. 解析URL：首先会对 URL 进行解析，分析所需要使用的传输协议和请求的资源的路径。如果输入的 URL 中的协议或者主机名不合法，将会把地址栏中输入的内容传递给搜索引擎。如果没有问题，浏览器会检查 URL 中是否出现了非法字符，如果存在非法字符，则对非法字符进行转义后再进行下一过程。
2. 缓存判断：浏览器会判断所请求的资源是否在缓存里，如果请求的资源在缓存里并且没有失效，那么就直接使用，否则向服务器发起新的请求。
3. DNS解析： 下一步首先需要获取的是输入的 URL 中的域名的 IP 地址，首先会判断本地是否有该域名的 IP 地址的缓存，如果有则使用，如果没有则向本地 DNS 服务器发起请求。本地 DNS 服务器也会先检查是否存在缓存，如果没有就会先向根域名服务器发起请求，获得负责的顶级域名服务器的地址后，再向顶级域名服务器请求，然后获得负责的权威域名服务器的地址后，再向权威域名服务器发起请求，最终获得域名的 IP 地址后，本地 DNS 服务器再将这个 IP 地址返回给请求的用户。用户向本地 DNS 服务器发起请求属于递归请求，本地 DNS 服务器向各级域名服务器发起请求属于迭代请求。
4. 获取MAC地址： 当浏览器得到 IP 地址后，数据传输还需要知道目的主机 MAC 地址，因为应用层下发数据给传输层，TCP 协议会指定源端口号和目的端口号，然后下发给网络层。网络层会将本机地址作为源地址，获取的 IP 地址作为目的地址。然后将下发给数据链路层，数据链路层的发送需要加入通信双方的 MAC 地址，本机的 MAC 地址作为源 MAC 地址，目的 MAC 地址需要分情况处理。通过将 IP 地址与本机的子网掩码相与，可以判断是否与请求主机在同一个子网里，如果在同一个子网里，可以使用 APR 协议获取到目的主机的 MAC 地址，如果不在一个子网里，那么请求应该转发给网关，由它代为转发，此时同样可以通过 ARP 协议来获取网关的 MAC 地址，此时目的主机的 MAC 地址应该为网关的地址。
5.  TCP三次握手： 下面是 TCP 建立连接的三次握手的过程，首先客户端向服务器发送一个 SYN 连接请求报文段和一个随机序号，服务端接收到请求后向客户端发送一个 SYN ACK报文段，确认连接请求，并且也向客户端发送一个随机序号。客户端接收服务器的确认应答后，进入连接建立的状态，同时向服务器也发送一个ACK 确认报文段，服务器端接收到确认后，也进入连接建立状态，此时双方的连接就建立起来了。
6. HTTPS握手： 如果使用的是 HTTPS 协议，在通信前还存在 TLS 的一个四次握手的过程。首先由客户端向服务器端发送使用的协议的版本号、一个随机数和可以使用的加密方法。服务器端收到后，确认加密的方法，也向客户端发送一个随机数和自己的数字证书。客户端收到后，首先检查数字证书是否有效，如果有效，则再生成一个随机数，并使用证书中的公钥对随机数加密，然后发送给服务器端，并且还会提供一个前面所有内容的 hash 值供服务器端检验。服务器端接收后，使用自己的私钥对数据解密，同时向客户端发送一个前面所有内容的 hash 值供客户端检验。这个时候双方都有了三个随机数，按照之前所约定的加密方法，使用这三个随机数生成一把秘钥，以后双方通信前，就使用这个秘钥对数据进行加密后再传输。
7. 返回数据： 当页面请求发送到服务器端后，服务器端会返回一个 html 文件作为响应，浏览器接收到响应后，开始对 html 文件进行解析，开始页面的渲染过程。 
8. 页面渲染： 浏览器首先会根据 html 文件构建 DOM 树，根据解析到的 css 文件构建 CSSOM 树，如果遇到 script 标签，则判端是否含有 defer 或者 async 属性，要不然 script 的加载和执行会造成页面的渲染的阻塞。当 DOM 树和 CSSOM 树建立好后，根据它们来构建渲染树。渲染树构建好后，会根据渲染树来进行布局。布局完成后，最后使用浏览器的 UI 接口对页面进行绘制。这个时候整个页面就显示出来了。 
9. TCP四次挥手： 最后一步是 TCP 断开连接的四次挥手过程。若客户端认为数据发送完成，则它需要向服务端发送连接释放请求。服务端收到连接释放请求后，会告诉应用层要释放 TCP 链接。然后会发送 ACK 包，并进入 CLOSE_WAIT 状态，此时表明客户端到服务端的连接已经释放，不再接收客户端发的数据了。但是因为 TCP 连接是双向的，所以服务端仍旧可以发送数据给客户端。服务端如果此时还有没发完的数据会继续发送，完毕后会向客户端发送连接释放请求，然后服务端便进入 LAST-ACK 状态。客户端收到释放请求后，向服务端发送确认应答，此时客户端进入 TIME-WAIT 状态。该状态会持续 2MSL（最大段生存期，指报文段在网络中生存的时间，超时会被抛弃） 时间，若该时间段内没有服务端的重发请求的话，就进入 CLOSED 状态。当服务端收到确认应答后，也便进入 CLOSED 状态。



## 其他

### 敏捷开发

敏捷开发是一种软件开发的思想流程，强调快速反应、快速迭代、价值驱动。



