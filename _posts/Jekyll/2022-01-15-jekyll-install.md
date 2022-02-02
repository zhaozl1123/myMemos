---
layout: post
title:  "在windows上安装Jekyll"
date:   2022-01-15 15:13:00 +0800
categories: [jekyll, windows-install]
tags: [jekyll, windows-install]
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

#### 1.安装RubyWithDevkit

下载安装exe，地址：[http://rubyinstaller.org/downloads/](https://link.jianshu.com?t=http://rubyinstaller.org/downloads/)

- 根据自己的机型选择对应的安装包(**因后续有需要安装不同的gem，我发现好多因为ruby版本问题装不了，所以在这推荐使用2,2,4版本的**)

测试是否安装完成：

```bash
ruby -v
```

#### 2.安装jekyll

先查看你的gem是否安装完毕：

```bash
gem -v
```

安装：

```bash
gem install jekyll
```

测试是否安装完毕：

```bash
jeckll -v
```

### 3.新建jekyll 项目

```bash
jekyll new myblog
cd myblog
```

### 4.运行jekyll 项目

- 官方文档（[http://jekyllrb.com/docs/quickstart/](https://link.jianshu.com?t=http://jekyllrb.com/docs/quickstart/)）

```bash
jekyll s  / jekyll serve
```

- 如果报错，按照提示，安装相关的gem

### 5.可能遇到的问题

**C:/Ruby30-x64/lib/ruby/gems/3.0.0/gems/jekyll-4.2.1/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- webrick (LoadError)**

- 可能的解决方案：bundle add webrick

**C:/Ruby30-x64/lib/ruby/gems/3.0.0/gems/jekyll-4.2.1/lib/jekyll/commands/serve/servlet.rb:3:in `require': cannot load such file -- bundler(LoadError)**

- 可能的解决方案：gem install bundler

**Could not find gem 'html-proofer (~> 3.18)' in locally installed gems**

- 可能的解决方案：bundle install --gemfile=Gemfile

