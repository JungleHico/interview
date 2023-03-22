# CSS 常见面试题



## 目录

- [HTML](../html/html.md)

- [CSS](../css/css.md)

- [JavaScript](../js/js.md)

- [笔试题](../code/code.md)

- [TypeScript](../typescript/typescript.md)

- [Vue](../vue/vue.md)

- [Webpack 和前端工程化](../webpack/webpack.md)

- [微信小程序](../mini-program/mini-program.md)



## CSS 选择器及优先级

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



## 常见的居中方式

1. `text-align: center` （文本水平居中）

2. `margin: 0 auto`（水平居中）
3. `line-height: 1em`（单行文本垂直居中）
4. 绝对定位：`position: absolute; top: 0; left: 0; transform: translate(-50%, -50%)`
5. 弹性布局：`display: flex; justify-content: center; align-items: center`



## 常见隐藏元素的方式

- `display: none`：元素会从文档树中删除，不会占据空间。
- `visibility: hidden`：元素仍然占据空间，但绑定的事件不生效。
- `opacity: 0`：元素的不透明度设为0，元素仍然占据空间且绑定的事件仍然生效。
- `position: absolute`：通过绝对定位，将元素设置到可视区域外。
- `z-index: -1`：通过其他元素将其盖住，来实现隐藏效果。



## transition 和 animation 的区别

- `transition`：用于定义 CSS 属性变化的效果，只涉及初始帧和结束帧，通常需要某个事件才能触发，例如点击（`:active`）、鼠标滑过（`:hover`）、聚焦（`:focus`）等。
- `animation`：可以更加灵活地定义动画，可以通过 `@keyframes` 定义多个动画帧，可以循环执行，不要事件就可以触发。



## 伪类和伪元素

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



## 盒模型

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



## 分辨率、像素比和视口

- 物理分辨率：屏幕的实际分辨率，常见的有 1920\*1080、2560\*1440 等。
- 逻辑分辨率和设备像素比：随着移动设备的屏幕分辨率越来越高，如果1个像素点只渲染1个像素点对应的内容，那么图片和文字就会显得非常小，为了解决这个问题，浏览器的**逻辑分辨率**就诞生了。浏览器通过一个倍率降低分辨率，达到人眼能够看到的更好的效果。例如一台手机的**物理分辨率**是 1920\*1080，浏览器以**逻辑分辨率** 640\*320 来渲染页面，也就是3个物理像素点渲染1个像素的内容，这个比率被称为**设备像素比**。浏览器的**设备像素比**可以通过 `window.devicePixelRatio` 来获取。
- 视觉视口：指用户通过屏幕可以看到的区域，一般等于浏览器窗口大小。
- 布局视口：指页面布局的基准窗口，一般 PC 端浏览器的布局视口与浏览器窗口大小相等，但在移动端，布局视口有一个默认值，约为 `964px`（布局视口大小可以通过 `document.documentElement.clientWidth / clientHeight` 来获取），这样用户需要左右滚动和缩放才能看到页面的完整内容。为了解决上面的问题，我们通常通过 `<meta>` 标签设置浏览器的布局视口大小等于视觉视口的大小。

![viewport](./assets/viewport.awebp)

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```



## 渐进增强和优雅降级

- 渐进增强：针对低版本浏览器进行构建页面，保证最基本的功能，然后再针对高级浏览器进行效果、交互等改进和追加功能达到更好的用户体验。
- 优雅降级：一开始就构建完整的功能，然后再针对低版本浏览器进行兼容。



## 重排和重绘

- **重排**：当页面元素的尺寸、结构等发生变化时，浏览器会重写渲染部分或者整个文档，由于浏览器渲染页面是基于流式布局的，所以会导致周围的元素重新排列。常见的会引起重排的操作有：元素的尺寸、位置、内容、字体等发生变化，触发 CSS 伪类，添加或删除元素等。
- **重绘**：当元素的样式发生变化时，浏览器会对其重新绘制，但不会影响其他元素的位置。**重排一定会触发重绘，重绘时不一定会重排**。



## CSS 性能优化

1. CSS 代码压缩；
2. 使用类名选择器代替标签选择器；
3. 避免使用通配符选择器（`*`）；
4. 后代选择器的层级不要超过三层；
5. 避免使用 `@import`；
6. 使用 `transition` 和 `animation` 代替 JS 实现简单的动画效果。



## SCSS 和 Less 等 CSS 扩展语言有哪些特性

变量、嵌套、混合、导入等。

