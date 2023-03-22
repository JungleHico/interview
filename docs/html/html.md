# HTML 常见面试题





## 目录

- [HTML](../html/html.md)

- [CSS](../css/css.md)

- [JavaScript](../js/js.md)

- [笔试题](../code/code.md)

- [TypeScript](../typescript/typescript.md)

- [Vue](../vue/vue.md)

- [Webpack 和前端工程化](../webpack/webpack.md)

- [微信小程序](../mini-program/mini-program.md)



## 块级元素和行内/内联元素

|          | 块级元素                                                     | 行内元素                                                     |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 特点     | 块级元素占据一行的空间                                       | 行内元素只占据内容的宽度                                     |
| 宽高     | 可以设置 `width` 和 `height`，`width` 默认 100%              | 设置 `width` 和 `height` 无效                                |
| 边距     | 可以设置 `margin` 和 `padding`                               | `margin` 和 `padding` 只能设置水平方向，不能设置垂直方向     |
| 常见标签 | `<div> <p> <h1> <form> <ol> <ul> <li> <audio> <video> <canvas>` | `<span> <a> <img> <button> <input> <label> <br> <i> <strong>` |



## src 和 href 的区别

`src` 和 `href` 都可以加载外部资源，区别在于：

- `src`：常用于 `<script>` 标签，会加载和解析资源，阻塞页面的渲染。
- `href`：常用于 `<link>` 和 `<a>` 标签，会并行下载资源，不会阻塞当前文档的加载。



## 为什么通常把 `<script>` 标签放在 `<body>` 的底部？

如果把 JS 文件放在 `<head>` 里，会阻塞页面的渲染，页面渲染需要等到 JS 文件下载、解析后，期间页面会呈现空白。



## HTML5 新特性

1. 新增语义化标签：`<header>`、`<footer>`、`<nav>`、`<aside>`、`<section>`、`<article>` 等。
2. 新增音频和视频标签：`<audio>` 和 `<video>`。
3. 本地化存储：`localStorage` 和 `sessionStorage`。
4. 支持 canvas。
5. 支持 web socket。
6. history API：`go`、`forward`、`back`、`pushstate`。



## b 标签和 strong 标签的区别、i 标签和 em 标签的区别

- `<strong>` 是语义化标签，表示加重语气，而 `<b>` 标签只用于加粗效果，不过浏览器一般都会将 `<strong>` 的默认样式设为加粗。
- `<em>` 是语义化标签，表示强调语气，而 `<i>` 标签只用于斜体效果，不过浏览器一般都会将 `<em>` 的默认样式设置为斜体。



## HTML5 语义化标签优点

1. 增加代码可读性和可维护性；
2. 有利于 SEO；
3. 对无障碍阅读友好，例如屏幕阅读器可以更好地读取页面信息。