title: "Rails 开发起步"
date: 2015-03-02 00:27:19
tags:
---

## 安装 Rails

如果是在 Windows 环境下开发，安装 [RailsInstaller](http://railsinstaller.org/en)。
Get to work，别折腾任何环境相关的问题。  RailsInstaller 安装完成后便有一个完整的 Rails 开发环境。

### 编辑器

首推 [RubyMine](https://www.jetbrains.com/ruby/)。一个良好的编辑器在起步时，如果使用恰当的情况将会是一个很不错的助手。

当对项目的结构有了一定的了解之后，可以考虑结合 [Atom](http://atom.io/)。智能 IDE 可以帮我们做很多事情，当熟悉之后，我们可以渐进的替换到轻量一些的编辑器上，加深对项目结构的理解。

Get to work，别折腾任何编辑器相关的问题。


<!--more-->


## 新建 Rails 应用

执行命令：

```
rails new <name>
```

其中 `name` 为应用的名称，例如新建 HelloRails 应用： `rails new HelloRails`。

> 执行 `rails new -h` 可以查看新应用生成器的所有命令行选项。

## Bundler

[Bundler](http://bundler.io/) 用于安装应用所需要的依赖包（gem），保证应用所使用的包软件一致。 执行 `rails new` 的时候会自动调用 `bundle install` 来安装依赖包。之后增添依赖包到 `Gemfile` 中，需要手动执行 `bundle install` 来安装。

### 安装依赖包

应用所使用的依赖包在 `Gemfile` 中指定，并使用命令 `bundle install` 来执行安装。例如，以下的 `Gemfile` ：

```
Source 'https://rubygems.org'
Gem 'nokogiri'
Gem 'rack', '~1.1`
Gem 'rspec`, :require => 'spec'
```

> 国内连接官方的 `RubyGems` 不太稳定，建议使用淘宝的 [RubyGems](http://ruby.taobao.org/) 镜像。

### 可执行的依赖包

设定完成 `Gemfile` 后即可执行以下命令来安装依赖包：

```
$ bundle install
```

如果依赖包中包含可以在命令行执行文件，需要使用 `bundle exec` 命令来调用。例如，调用 `rspec` ：

```
$ bundle exec rspec spec/models
```

在某些情况下，没有通过 `bundle exec` 来调用亦可正常执行可执行文件。但这种情况只有在系统已经安装哪个可执行文件，并且这个系统级别的可执行文件所依赖的包没有跟应用内的依赖包产生冲突。不建议采用这种方式来调用可执行文件。

使用 `bundle exec` 来调用可执行 `gem` 会显得比较麻烦，所以 bundler 提供一种方式来减少这种输入。在安装依赖包的时候，加上 `--binstubs` 参数，即：

```
$ bundle install --binstubs
```

通过这种方式依赖安装包，可执行的包将被安装到 `bin` 目录下，并可以通过 `bin/<executable>` 来调用。例如，执行 `rspec` ：

```
$ bin/rspec spec/models
```


## Hello, Rails

Rails 自带一个脚本，用于启动本地服务器 WEBrick，方便开发工作。这个命令是：

```
$ rails server
```

当启动完成后将自动在 `0.0.0.0:3000` 监听所有的 http 请求。如果需要更改端口或者 IP，则需要传入特定的参数：

```
$ rails server -b <ip> -p <port>
```

在浏览器中输入 `http://<ip>:<port>` 即可访问 Rails 应用本地服务器。
使用 `ctrl + c` 来终止此本地服务器。
