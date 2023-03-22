# Vue 常见面试题



## 目录

- [HTML](../html/html.md)

- [CSS](../css/css.md)

- [JavaScript](../js/js.md)

- [笔试题](../code/code.md)

- [TypeScript](../typescript/typescript.md)

- [Vue](../vue/vue.md)

- [Webpack 和前端工程化](../webpack/webpack.md)

- [微信小程序](../mini-program/mini-program.md)



## MVVM 

M（`Model`），即数据模型；V（`View`），即视图。

传统的开发模式，例如原生 JS 或者 jQuery，视图和模型是不分离的，更新数据时需要先找到视图，即需要更新数据的元素，这种方式当业务逻辑变得复杂之后就会难以维护。

MVVM 实现了模型和视图的分离，通过 MV（`ViewModel`），将数据与视图绑定，更新数据时会自动更新视图，视图变化时也会通知 ViewModel 更新数据。



## Vue 3 响应式数据的基本实现

Vue 2 中使用 `Object.defineProperty()` 来实现对对象属性的读取和设置，Vue 3 中采用 ES6 的 [Proxy](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 语法。**Proxy 是一个对象，它包装了另一个对象，并允许你拦截对该对象的任何交互。** 通过 Proxy 对数据的读取和设置进行拦截，当读对象的属性时，触发 `get` 函数，将副作用函数存入集合中；当设置对象的属性时，触发 `set` 函数，从集合中取出副作用函数并执行，这样就实现了简单的响应式数据。



## Vue3 新特性

1. 引入组合式 API，使业务逻辑关注点更加集中，提高代码复用性和可维护性。
2. 更好的 TS 支持。
3. 新增 `<Teleport>` 组件，可以将插槽内容渲染到指定外层 DOM。
4. Fragments，支持多根节点，减少节点层数，提高渲染性能。
5. 重构响应式系统，使用 `Proxy` 代替 Vue 2 的 `Object.defineProperty` 实现响应式数据。
6. 新增静态标记（patchFlag）（编译器），提高渲染效率（渲染器）。



## 为什么 data 选项需要通过一个函数返回一个对象？

如果 `data` 直接指定一个对象，那么多个组件就会引用同一个数据，一个组件修改数据会污染其他组件的数据。通过一个函数返回数据对象，可以通过函数作用域进行隔离。



## v-if 和 v-show

`v-if` 是**真实**的条件渲染，是**惰性**的，只有当表达式的值为 `true` 时才会被渲染，当表达式的值为 `false` 时不会渲染，并且会销毁原有的元素。

`v-show` 元素始终会被渲染，只是通过 CSS 的 `display` 属性控制元素的显示与隐藏。

`v-if` 具有更高的切换开销，而 `v-show` 具有更高的初始化渲染开销。



## 为什么不推荐同时使用 v-for 和 v-if（v-for 和 v-if 优先级）

- Vue 2 中 `v-for` 的优先级比 `v-if` 高，`v-if` 会重复运行在每个 `v-for` 循环中，如果想要有条件的跳过循环，则可以将 `v-if` 至于外层；
- Vue 3 中 `v-if` 的优先级比 `v-for` 高，这意味着 `v-if` 无法访问 `v-for` 的作用域内的变量。



## 为什么推荐为 v-for 提供 key

Vue 默认按照“就地更新”的策略来更新通过 `v-for` 渲染的元素列表。当数据项的顺序改变时，Vue 不会随之移动 DOM 元素的顺序，而是就地更新每个元素，确保它们在原本指定的索引位置上渲染。

默认模式是高效的，但**只适用于列表渲染输出的结果不依赖子组件状态或者临时 DOM 状态 (例如表单输入值) 的情况**。

为每个元素指定唯一的 `key` 属性，Vue 执行 Diff 算法更新节点时，就可以根据标识重用和重新排列现有元素。



## 为什么 Vue 3 的 setup 函数中不能使用 this？

因为 `setup` 函数在组件创建之前执行，所以 `setup` 函数中的 `this` 并不是组件实例的引用，因此应当避免在 `setup` 函数中使用 `this`。



## 如何理解 Vue 的单向数据流

所有的 props 都遵循着**单向绑定**原则，props 因父组件的更新而变化，自然地将新的状态向下流往子组件，而不会逆向传递。这避免了子组件意外修改父组件的状态的情况，不然应用的数据流将很容易变得混乱而难以理解。



## computed 和 watch

1. `computed` **支持缓存**，只在相关响应式依赖发生改变时，才会重新求值；`watch` **不支持缓存**，只要数据发生变化，就会执行侦听函数。
2. `computed` 的职责仅为计算和返回值，不应该有其他副作用（**异步请求或更改 DOM**）；`watch` 相对更加通用，**适合执行异步或者开销较大的操作**。



## vue 组件传参方法

1. 父组件通过 `props` 传数据给子组件
2. 子组件通过 `emit` 自定义事件传递数据
3. 祖先组件通过 `provide` 传递数据，后代组件通过 `inject` 接受数据
4. 父组件通过 `refs` 获取子组件实例
5. Vue 2 eventBus
6. 状态管理 Vuex/Pinia



## Vue 3 中代码复用的方式

1. **组件**：构建模块和 HTML 代码的复用
2. **组合式函数**：逻辑（JS 代码）的复用，例如把某个业务封装到 `useXXX()` 函数中然后导出。
3. **自定义指令**：复用 HTML 元素的 DOM 操作，比如元素自动聚焦、图片懒加载。



## Vue 3 内置组件

- Transition、TransitonGroup
- KeepAlive
- Teleport



## keepAlive

`<keep-alive>` 是 Vue 的一个内置组件，可以缓存组件，当组件切换时不会被销毁。

- `<keep-alive>` 默认会缓存所有组件，可以通过 `include/exclude` 控制要缓存的组件。
- 可以通过 `onActivated()` 和 `onDeactivated` 生命周期监听组件的显示/隐藏。



## vue-router history 模式和 hash 模式

|            | hash 模式                                                    | history 模式                                                 |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| url        | 包含哈希符号 `#`                                             | 不包含 `#`                                                   |
| 无刷新实现 | 通过 `window.onhashchange` 来监听 `hash` 的变化，借此实现无刷新跳转 | 通过 `history.pushState` 和 `history.replaceState` 来实现无刷新跳转 |
| 服务器配置 | 不需要服务器层面做处理                                       | 服务器需要配置回退路由，否则会出现刷新页面404的问题          |
| SEO        | `hash` 模式的页面跳转都在客户端中，不利于 SEO                | SEO 友好                                                     |



## Vue 路由守卫

- 全局路由守卫：`beforeEach`、`beforerResolve`、`AfterEach`
- 路由独享守卫：`beforeEnter`
- 组件内守卫：`beforeRouteEnter`、`beforeRouteUpdate`、`beforeRouteLeave`



## Vue 源码解析

[JungleHico/vue-source: Vue3 源码解析与实现，包含响应系统、渲染器和组件化 (github.com)](https://github.com/JungleHico/vue-source)

