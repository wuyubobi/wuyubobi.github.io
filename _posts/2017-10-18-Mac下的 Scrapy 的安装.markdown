---
layout:     post
title:      Python爬虫学习-Mac安装Scrapy
subtitle:   Python 学习历程
date:       2017-10-18
author:     "ZhangBo"
header-img: "img/post-bg-gongju.jpg"
catalog: true
tags:
- 爬虫
- Python
- Scrapy
---
### Python爬虫学习

#### Mac 安装 Scrapy

基于 python2.7版本

主要步骤:
1. 安装homebrew(已安装可跳过)
	- ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
2. 安装 wget(已安装可跳过)
	- brew install wget
3. 安装 command line tools
	- xcode-select —install
4. 安装 python pip 
	-  wget https://bootstrap.pypa.io/get-pip.py
	-  python get-pip.py
	- 如果之前安装过可以通过 sudo pip install --upgrade pip 更新 pip
5. 当MAC系统版本高于10.11 需要关闭 SIP(系统完整性保护)
	- 电脑重启 开机过程中按住 command+r 键 直到出现苹果 logo + 进度条(在开启启动声音之前按住, 否则无法进入)
	- 进入恢复模式 提示选择语言
	- 通过左上方条目中的实用工具 打开终端选项
	- 输入命令 csrutil disable 关闭系统完整性保护( csrutil enable 开启)
	- 得到 Successfully disabled System…. 反馈后重启
6. 安装 Scrapy
	- sudo -H pip install Scrapy
	- scrapy version 如果返回 Scrapy 对应的版本既安装成功

#### 遇到的问题

1. Operation not permitted:
	- 这里分两种情况
		1. 原本命令前有 sudo 结果仍是这个错误 可能的原因就是你的 mac 版本高于10.11 需要关闭系统的完整性保护(关闭方式见上)
		2. 普通命令因权限不够无法执行 命令前面加上 sudo
2. If executing pip with sudo, you may want sudo's -H flag.
	-  命令前面加 sudo -H (H 大写)
	-  加 -H 后出现上方错误同1解决方式即关闭 SIP
3. 正确安装 Scapy 后 通过 scrapy version 检验安装结果时出现'module' object has no attribute 'OP\_NO\_TLSv1\_1'\_
	- 可能由于twisted版本过高导致 可通过sudo pip install twisted==13.1.0 降低 twisted 版本解决