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

##### Ubuntu 安装 YouCompleteMe

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
		` 
	Bundle 'Valloric/YouCompleteMe'
	" youcompleteme  默认tab  s-tab 和自动补全冲突
	" let g:ycm_key_list_select_completion=['<c-n>']
	" let g:ycm_key_list_select_completion = ['<Down>']
	" let g:ycm_key_list_previous_completion=['<c-p>']
	" let g:ycm_key_list_previous_completion = ['<Up>']
	set completeopt=longest,menu
	let g:ycm_confirm_extra_conf=0      " 关闭加载.ycm_extra_conf.py提示
	let g:ycm_complete_in_comments = 1  "在注释输入中也能补全
	let g:ycm_complete_in_strings = 1   "在字符串输入中也能补全
	let g:ycm_collect_identifiers_from_tags_files=1                 " 开启 YCM 基于标签引擎
	let g:ycm_collect_identifiers_from_comments_and_strings = 1   "注释和字符串中的文字也会被收入补全
	let g:ycm_seed_identifiers_with_syntax=1   "语言关键字补全, 不过python关键字都很短，所以，需要的自己打开
	let g:ycm_collect_identifiers_from_tags_files = 1
	let g:ycm_min_num_of_chars_for_completion=2                     " 从第2个键入字符就开始罗列匹配项
	let g:ycm_path_to_python_interpreter='/usr/bin/python'
	" 引入，可以补全系统，以及python的第三方包 针对新老版本YCM做了兼容
	" old version
	if !empty(glob("~/.vim/bundle/YouCompleteMe/cpp/ycm/.ycm_extra_conf.py"))
		let g:ycm_global_ycm_extra_conf = "~/.vim/bundle/YouCompleteMe/cpp/ycm/.ycm_extra_conf.py"
	endif
	" new version
	if !empty(glob("~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp/ycm/.ycm_extra_conf.py"))
		let g:ycm_global_ycm_extra_conf = "~/.vim/bundle/YouCompleteMe/third_party/ycmd/cpp/ycm/.ycm_extra_conf.py"
	endif

	"mapping
	nmap <leader>gd :YcmDiags<CR>
	nnoremap <leader>gl :YcmCompleter GoToDeclaration<CR>           " 跳转到申明处
	nnoremap <leader>gf :YcmCompleter GoToDefinition<CR>            " 跳转到定义处
	nnoremap <leader>gg :YcmCompleter GoToDefinitionElseDeclaration<CR>
	" 直接触发自动补全
	let g:ycm_key_invoke_completion = '<C-Space>'
	" 黑名单,不启用
	let g:ycm_filetype_blacklist = {
		  \ 'tagbar' : 1,
		  \ 'gitcommit' : 1,
		  \}  
	`
5. 其他插件推荐
	- delimitMate：括号补全
	- indentLine：显示缩进对齐