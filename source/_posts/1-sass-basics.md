title: "Sass 基础"
date: 2016-01-28 14:45:45
tags:
  - Sass
description: 介绍 Sass 的基础知识，包含 变量、嵌套、局部模板、导入、Mixin、扩展/集成以及操作符。
---

当一个项目超过一定的规模后，CSS 容易变得难于维护。CSS 预处理语言便由此而生，目的在于解决 CSS 的局限。通常一门 CSS 预处理语言会提供一些编程语言常见的特性，例如：变量、嵌套、函数、继承等，而后通过特定的处理工具转换成普通的 CSS 文件。 Sass 正是预处理语言中的一种。

## 安装  Sass

Sass 预处理依赖于  Ruby，因此在使用 Sass 之前需要先准备 Ruby 环境。当 Ruby 环境安装就绪后，既可以使用 Gem 来安装 Sass：

```
gem install sass
```

上述命令执行成功后，使用 `sass -v` 来确认安装的 sass 版本，命令输出结果类似于 `Sass 3.4.12 (Selective Steve)`。Sass 成功安装之后，我们即可在命令行下使用 `sass` 来将 `sass` 文件转换成普通的 `css` 文件，命令如下：

```
sass input.sass output.css
sass --watch app/sass:public/stylsheets
```

代码中包含了一个 `--watch` 选项，借助于此选项我们可以监视目录，在文件有变动的时候自动进行转换，这个特性对于尝试 Sass 非常方便。而在正常的项目开发中，我们通常使用构建工具，将这个转换过程放置在构建流程中。

## 变量 (Variables)


变量用于存储特定的值，以便于在代码中多处应用。在 Sass 中，变量以美元符号 `$` 开头，可以存储 颜色值、字体簇、背景图片地址等 CSS 规则的值。示例：

```
$font-stack: Hevetica, sans-serfi
$primary-color: #333

body
  font: 100% $font-stack
  color: $primary-color
  
// 转换后的 CSS 如下
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}
  
```

变量的强大之处在于通过设定不同变量的值，即可提供不同的外观。

## 嵌套 (Nesting)

HTML 是一种结构化标记语言，节点之间有着清晰的嵌套结构，但 CSS 并没有提供这种嵌套的功能。因此，Sass 提供类似于这种嵌套的特性，类似于 HTML。
但由于 CSS 的规则权重计算的关系，过度的嵌套会使得权重难于计算与维护，所以这个特性是一把双刃剑。尽量保持嵌套层级不要超过三层。

嵌套实例：

```
nav
  ul
    list-style: 0
    
  li
    display: inline-block
    
  a
    display: block
    padding: 6px 12px
    
// 转后的 CSS 如下：
nav ul {
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

## 局部文件 (Partials)