# Webpack 和前端工程化



## 目录

- [HTML](../html/html.md)

- [CSS](../css/css.md)

- [JavaScript](../js/js.md)

- [笔试题](../code/code.md)

- [TypeScript](../typescript/typescript.md)

- [Vue](../vue/vue.md)

- [Webpack 和前端工程化](../webpack/webpack.md)

- [微信小程序](../mini-program/mini-program.md)

- [计算机网络](../network/network.md)



## Webpack

[[JungleHico/webpack-doc: webpack 使用文档 (github.com)](https://github.com/JungleHico/webpack-doc)]([JungleHico/webpack-doc: webpack 使用文档 (github.com)](https://github.com/JungleHico/webpack-doc))



## Webpack 打包过程

1. 初始化参数：从配置文件和 Shell 语句中读取与合并参数，得出最终的参数。
2. 开始编译：用上一步得到的参数初始化 Compiler 对象，加载所有配置的插件，执行对象的 run 方法开始执行编译。
3. 确定入口：根据配置中的 entry 找出所有的入口文件。
4. 编译模块：从入口文件出发，调用所有配置的 Loader 对模块进行翻译，再找出该模块依赖的模块，再递归本步骤直到所有入口依赖的文件都经过了本步骤的处理。
5. 完成模块编译：在经过第 4 步使用 Loader 翻译完所有模块后，得到了每个模块被翻译后的最终内容以及它们之间的依赖关系。
6. 输出资源：根据入口和模块之间的依赖关系，组装成一个个包含多个模块的 Chunk，再把每个 Chunk 转换成一个单独的文件加入到输出列表，这步是可以修改输出内容的最后机会。
7. 输出完成：在确定好输出内容后，根据配置确定输出的路径和文件名，把文件内容写入到文件系统。



## Webpack Loader 和 Plugin

|          | Loader                                                       | Plugin                                                       |
| -------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| 作用     | webpack 默认只支持编译 js 模块，而通过 loader，webpack 可以支持各种语言和预处理器编写模块。 | plugin 可以以扩展 webpack 的功能，让 webpack 具有更多的灵活性。 |
| 加载顺序 | 从后往前                                                     | 从前往后                                                     |



## 开发环境和生产环境

开发环境（`development`）和生产环境（`production`）的构建目标差异很大。

- 在开发环境中，我们需要具有强大的、具有实时重新加载（live reloading）或热模块替换（hot module replacement）能力的 source map 和 localhost server。
- 在生产环境中，我们的目标则转向于关注更小的 bundle，更轻量的 source map，以及更优化的资源，以改善加载时间。



## source-map

当 webpack 打包源代码时，可能会很难追踪到错误和警告在源代码中的原始位置。为了更容易地追踪错误和警告，JavaScript 提供了 source map 功能，将编译后的代码映射回原始源代码。webpack 通过 `devtool` 属性来配置不同的 `source-map` 值。使用不同的 `source-map` 值，代码的构建速度和代码映射是不一样的。

- 对于开发环境，通常希望以增加编译后包的体积为代价，获取编译较快速且调试友好的 source map。
- 但是对于生产环境，则希望分离和压缩模块，获得体积较小且不能有原始源代码（可以有行列信息供调试）的 source map。



## Webpack 构建优化

1. 对于生产环境，可以通过 `webpack-bundle-analyzer` 插件将打包后的结果以矩形树图的方式进行可视化显示，方便我们进行模块分析和性能优化。
2. 通过设置 `source-map` 的值，使开发环境的打包速度更快，生产环境的打包体积更小。
3. 通过 `thread-loader`，利用多线程进行打包。
4. 通过 `externals` 属性，以外部扩展的形式引入代码库，这样就可以通过 CDN 进行加速了。 
5. Tree-Shaking，webpack 自带，可以剔除不需要用到的代码。



## 浏览器缓存和代码分离



## 权限控制

路由权限（菜单权限）、接口权限、动作权限



## CI/CD

- CI：持续集成，包含代码提交和自动化测试

- CD：持续部署，一般指自动化部署

CI/CD 一般指项目的自动化，常见的方案有 Github Actions、Gitlab Runner 和 Jenlins 等。



### Github Actions

参考：[Github Action自动化部署](https://www.bilibili.com/video/BV1Ca411h7rx/?spm_id_from=333.999.0.0&vd_source=82bae426e35bb536955cd65831b6f5d8)，创建和配置工作流配置文件 `.github/workflows/main.yml`，当 Github 仓库 `push` 新代码时，自动检查 Node 环境，运行安装项目依赖和项目构建命令，并打包上传到服务器，实现自动化部署。



### Gitlab Runner

1. 服务器安装 Gitlab Runner
2. 服务器注册 Gitlab Runner（需要获取 token，token 分为整个平台、团队和项目3个级别）
3. 项目根目录创建 `.gitlab-ci.yml` 配置文件，指定构建、测试和部署脚本。



## npm 私服

搭建 npm 私服可以提高项目依赖下载速率，也可以管理企业自研的开发包。搭建 npm 私服一般通过 [Verdaccio](https://verdaccio.org/zh-cn/docs/what-is-verdaccio/)。



## 微前端

微前端借鉴了微服务的概念，将一个庞大的应用拆解成若干个独立开发（技术栈独立）、独立运行、松散耦合的应用。常见的微前端框架有：[qiankun]([qiankun - qiankun (umijs.org)](https://qiankun.umijs.org/zh))、[MicroApp]([MicroApp (micro-zoe.github.io)](https://micro-zoe.github.io/micro-app/))、[无界]([无界 | 极致的微前端框架 (wujie-micro.github.io)](https://wujie-micro.github.io/doc/)) 等。