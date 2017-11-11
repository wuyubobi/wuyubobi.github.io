---
layout:     post
title:      pyspider练习(妹子图(meizitu)网站的图片爬取)
subtitle:   Python 学习历程
date:       2017-10-26
author:     "ZhangBo"
header-img: "img/post-bg-js-ad-keep.jpg"
catalog: true
tags:
- pyspider
- Python3
- Mac
---
### pyspider 练习

#### 妹子的图片爬取

基于 Mac版本 Window Linux大同小异

主要步骤:
1. 准备工作
	- 安装 pyspider
		1. Mac 下 sudo pip3 install pyspider
		2. Ubuntu 先提前检查 sudo apt-get install python python-dev python-distribute python-pip libcurl4-openssl-dev libxml2-dev libxslt1-dev python-lxml 后 sudo pip3 install pyspider
		3. 当爬取的页面需要JS 动态解析生成时需要安装phantomjs
			-  Mac brew install phantomjs
			-  Ubuntu sudo apt-get install phantomjs
2. 创建 pyspider项目
	 - 命令行 pyspider all 启动所有组件
	- 启动成功后 访问 localhost:5000可以看到 pyspider的主页面
	- 点击右侧的 Create创建一个项目 此时你已成功的创建了一个 pyspider 的项目
3. 对目标页面进行分析
	- [妹子图][1] 首页有大图 点击第二页以后 url 变为 http://www.meizitu.com/a/more\_1.html 首页的图片也存在与第二页 那么意味着我们从第二页开始爬取即可爬到整站的图片
	- 通过点击第二页 第三页发现 url 的变化仅为 more后面的数值发生变化
	- 提取目标的 url 通过 Chrome 浏览器审查元素可发现每一组的 url 位于 li \> div \> .pic \> a 标签的 href 属性中
	- 进入详情页 目标图片 位于 #picture \> p \> img 的 src 属性 图片的名字 为 alt 属性
	- 网页的名字 h2 \> a 的 text() 方法取出
	- 由于妹子图的图片有防盗链机制, 当我们点击图片的时候发现Referer : http://www.meizitu.com/a/5585.html 后面的对应图片所在的详情页 (Referer 在请求头中表示此图片来源于哪) 所以我们在下载图片的时候需要在请求头中加入 Referer 
4. 开始撸码
	-  [具体代码][2]
5. 成果
	![][image-1]

#### 遇到的问题

1. 图片的防盗链机制, 一直爬到的都是防盗链的图片
	- 通过 Chrome 浏览器监测请求, 查看正常返回时的请求头与异常时的请求头的不同
2. 不能依赖pyspider 自带的 css selecter helper 有时选择会偏差
3. 没有代码提示, 和代码监测 
	- 平时多注意完整 api 的书写
	- 记不住的可以在 IDE 中编写后复制过来







[1]:	http://www.meizitu.com
[2]:	http://op0s30etn.bkt.clouddn.com/MeiZiTuSpider.py

[image-1]:	http://op0s30etn.bkt.clouddn.com/meizitu.jpg