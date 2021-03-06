# Css的polyfill杂谈

Css的特性和Js一样让人烦恼，前端开发者都面临着兼容各种浏览器的问题，但幸运的是这两者都有各自的解决方案。

## JavaScript

对于JavaScript，我们有Babel和Polyfill，但是这两者又有很大的差别，我们可以简单的理解为：

- Babel：转换不兼容的语法
- Polyfill：转换不兼容的API

## Css

对于Css，我们可以使用`POSTCSS`这玩意在构建阶段给你添加一堆前缀来兼容不同浏览器

## 问题

> 为什么CSS的Polyfill比较难？

因为JavaScript是动态语言，它的意义取决于它执行时的上下文，在运行时我们可以改变它的结构。当我们引入Polyfill后，我们的Js在运行时就可以动态的从其中获取解决方案；但是对于Css，很明显它是静态的，我们大多数情况下在构建阶段对其进行兼容性修改…

了解浏览器渲染机制的都知道，渲染引擎同时解析HTML文档和样式(CSS和Style中)，两者分别生成DOM树和CSSOM树，再之后构成渲染树，在这个过程中你是无法控制渲染和CSSOM生成的，你能控制的只有DOM。

但庆幸的是我们还能控制DOM，并且以此来控制CSSOM，但是这种代价是很大的。我们需要遍历DOM来找到我们的目标标签进行解析，重写——这意味着更新DOM，那么就会带来一系列的重绘重排过程。

如今绝大多数的CSS polyfill都包含了它们自己的CSS解析器以及运行逻辑。与此同时，由于解析和运行都是非常复杂的事情，所以这些polyfill要么太大，要么太容易有bug。

所以如果你希望浏览器去做一些它并不懂如何去做的工作（比如使用你的自定义CSS），那么你必须伪装一些指令给浏览器。

## 可能的解决方案？

[Houdini](https://github.com/w3c/css-houdini-drafts/wiki)
