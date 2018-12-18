---
layout: post
title: "MAC下安装jekyll步骤及问题"
categories: 软件安装
tags: jekyll
author: candoy
---

* content
{:toc}



#MAC下安装jekyll步骤及问题

MAC系统10.14.2，在使用gem install jekyll出现以下问题
http_parser.rb-0.6.0/ext/ruby_http_parser 


试了很多种方法都没有解决这个问题，最后是参考这个文档

[Install Jekyll on macOS Mojave](https://desiredpersona.com/install-jekyll-on-macos/)


##一.安装步骤如下
###1.换源-使用国外的源，比较快
``
$ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
``

$ gem sources -l

https://gems.ruby-china.com
```# 确保只有 gems.ruby-china.com
```
###2.安装jekyll,出现问题
make  clean  c/gems/http_parser.rb-0.6.0/ext/ruby_http_parser 
make "DESTDIR=" 
make: *** No rule to make target `/System/Library/Frameworks/Ruby.framework/Versions/2.3/usr/include/ruby-2.3.0/universal-darwin18/ruby/config.h', needed by `ruby_http_parser.o'.  
Stop.  make failed, exit code 2

解决方案:
使用brew重新安装ruby,并设置新的ruby生效

1.安装ruby
brew install ruby
2.更新ruby的安装目录，加入到运行环境
echo 'export PATH="/usr/local/opt/ruby/bin:$PATH"' >> ~/.bash_profile
3.更新gem的目录，
echo 'export PATH=$HOME/gems/bin:$PATH' >> ~/.bash_profile
4.安装jekyll
gem install jekyll
gem install github-pages
