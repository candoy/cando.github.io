---
layout: post
title: "MAC下安装github.io+jekyll及使用问题"
categories: 软件安装
permalink: /jekyll_install_and_use_on_mac.html
tags: jekyll
author: candoy
---

**介绍jekyll的安装和使用，问题及解决方法。**

<!--more-->



* content
{:toc}

# 一、MAC安装jekyll

   参考以下文档：
  - [Install Jekyll on macOS Mojave](https://desiredpersona.com/install-jekyll-on-macos/)
  - [Jekyll博客系统初探](https://www.jianshu.com/p/558a5d50e077)

## 1.1 换源-使用国内源

{% highlight linux %}
$ gem sources --add https://gems.ruby-china.com/
$ gem sources -l
https://gems.ruby-china.com
{% endhighlight %}

  >确保只有 gems.ruby-china.com

## 1.2 安装jekyll

{% highlight linux %}
#gem install jekyll
#gem install github-pages
{% endhighlight %}

如果出现make failed
{% highlight linux %}
make  clean  c/gems/http_parser.rb-0.6.0/ext/ruby_http_parser
make "DESTDIR="
make: *** No rule to make target `/System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/include/ruby-2.3.0/universal-darwin18/ruby/config.h', needed by `ruby_http_parser.o'.  
Stop.  make failed, exit code 2
{% endhighlight %}

## 1.3 make安装失败解决
解决方案:
使用brew重新安装ruby,并设置新的ruby生效

1.安装ruby
{% highlight linux %}
#brew install ruby
{% endhighlight %}
2.更新ruby的安装目录，加入到运行环境
{% highlight linux %}
#echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
{% endhighlight %}
3.更新gem的目录
{% highlight linux %}
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bash_profile
{% endhighlight %}


安装其它包
{% highlight  bash %}
gem install jekyll // 安装jekyll
gem install kramdown // markdown语言解析包
gem install pygments.rb // 代码高亮包
gem install liquid
{% endhighlight %}
 //
// 还有些别的包，看需要来安装啦

# 二、jekyll使用

## 2.1 jekyll目录结构
{% highlight  bash %}
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── css
|── images
├── _site
└── index.html  
{% endhighlight %}

* _config.yml用来保存一些配置数据;

* _drafts目录用来存储草稿，与已经发布的文章不同，这是没有日期的文章，在运行jekyll serve会自动赋予当前日期。已经发布的文章在_posts目录下。

* _includes目录中包含的html文件可以作为模块来加载,比如加载footer.html可以使用标签{``%  %``}将代码include footer.html包裹其中来加载,这些代码被称作Liquid代码，在Jekyll中大量使用这种语法
正如上面所说_posts中放的是发布的文章，不过格式一定要符合年-月-日-标题.md否则会有错误。

* _layouts这里存放文章的模板,default.html是整个网站的框架，post.html则是单个文章的模板。

## 2.2 配置文件

## 2.3 代码高亮

## 2.4 发布POST

文件名格式：yyyy-mm-dd-post-name.md或者yyyy-mm-dd-post-name.markdown
在开始写具体内容前，必须填写yaml头信息，这样该文件才能被Jekyll进行处理。头信息必须在文件的开始部分，并且按照yaml的格式，如本篇文章：
{% highlight  bash %}
---
layout:     post
title:      "我的博客搭建记"
subtitle:   Hello World, Hello Blog
date:       2017-01-24
author:     "Tristan"
header-img: "img/post-bg-unix-linux.jpg"
catalog:    true
tags:
- 操作流
- 日志
---
{% endhighlight %}

## 2.5 网站计数器
