---
layout:     post
title:      Ubuntu 下 Vim补全神器YouCompleteMe安装
subtitle:   Python 学习历程
date:       2017-10-21
author:     "ZhangBo"
header-img: "img/post-bg-unix-linux.jpg"
catalog: true
tags:
- YouCompleteMe
- Python
- Ubuntu
---
### Vim 自动补全工具的安装

#### Ubuntu 安装 YouCompleteMe

基于 Ubuntu16.04版本

主要步骤:
1. 安装前的准备工作
	- vim 版本需大于7.3584, 并支持 python2脚本 
		1. 可以通过 vim —version 查看 vim 版本
		2. vim 安装 sudo apt-get install vim
		3. Python 安装 sudo apt-get install python-dev libxml2-dev libxslt-dev
	- 安装 git (sudo apt-get install git)
	- 安装 gcc (sudo apt-get install gcc)
	- 安装 cmake (sudo apt-get install cmake)
2. 安装 vim 的插件管理器Vundle
	 - `git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim (目标地址, 根据个人洗好更改) `
	- 这里可以通过Vundle 安装 YouCompleteMe (个人不推荐)
3. 通过 Git 安装YouCompleteMe
	- `git clone --recursive https://github.com/Valloric/YouCompleteMe.git ~/.vim/bundle/YouCompleteMe`
	- `cd ~/.vim/bundle/YouCompleteMe`
	- `git submodule update --init --recursive` 检查完整性 (如果缺少包的情况下, 会去下载相应的文件, 有可能超时, 反复执行, 直到所有包都下载完毕)
	- `./install.py --clang-completer` 在YouCompleteMe下执行, 时间较长 有 C 语言的提醒, 期间如果提示缺少什么就使用 apt-get 安装什么
4. YouCompleteMe的配置信息
	- 配置在`~/.vimrc`中
	- [详细配置信息][1]
5. 其他插件推荐
	- delimitMate：括号补全
	- indentLine：显示缩进对齐

[1]:	http://op0s30etn.bkt.clouddn.com/Ubuntu_YCM.txt