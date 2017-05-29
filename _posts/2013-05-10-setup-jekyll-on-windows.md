---
layout: post
title: "在 Windows 上安装 Jekyll 3"
description: "如何在 Windows 上安装 Jekyll 3"
categories: [笔记]
tags: [jekyll, ruby, windows]
redirect_from:
  - /2013/05/10/
last_updated: 2017年1月7日
---

> 若想查看原文，请点击[本链接](http://yizeng.me/2013/05/10/install-jekyll-3-on-windows/)。
>
> 最近更新于 - 2017年1月7日

* Kramdown table of contents
{:toc .toc}

## 安装 Ruby
{: #install-ruby}

1. 前往 <http://rubyinstaller.org/downloads/>

2. 在 "RubyInstallers" 部分，选择某个版本点击下载。<br />
   例如，`Ruby 2.3.3-p222 (x64)` 是适于64位 Windows 机器上的 Ruby 2.3.3 x64 安装包。

3. 通过安装包安装

	- 最好保持默认的路径 `C:/Ruby23-x64`，
	  因为安装包明确提出 “请不要使用带有空格的文件夹 (如： Program Files)”。
	- 勾选 "Add Ruby executables to your PATH"，这样执行程序会被自动添加至 PATH 而避免不必要的头疼。

	<a class="post-image" href="/assets/images/posts/2013-05-11-ruby-installer.png">
	<img itemprop="image" data-src="/assets/images/posts/2013-05-11-ruby-installer.png" src="/assets/javascripts/unveil/loader.gif" alt="Windows Ruby 安装包" />
	</a>

4. 打开一个命令提示行并输入以下命令来检测 Ruby 是否成功安装。

	> ruby -v

	输出示例：

	> ruby 2.3.3p222 (2016-11-21 revision 56859) [x64-mingw32]

## 安装 DevKit
{: #install-devkit}

DevKit 是一个在 Windows 上帮助简化安装及使用 Ruby C/C++ 扩展如 RDiscount 和 RedCloth 的工具箱。
详细的安装指南可以在程序的 [wiki 页面][Full installation instructions] 阅读。

1. 再次前往 <http://rubyinstaller.org/downloads/>

2. 下载同系统及 Ruby 版本相对应的 DevKit 安装包。
   例如，DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe 适用于64位 Windows 系统上的 Ruby 2.3.3 x64。

	下面列出了如何选择正确的 DevKit 版本：

	> **Ruby 1.8.6 to 1.9.3**: DevKit tdm-32-4.5.2<br />
	> **Ruby 2.0.0**: DevKit mingw64-32-4.7.2<br />
	> **Ruby 2.0.0 x64**: DevKit mingw64-64-4.7.2

3. 运行安装包并解压缩至某文件夹，如 C:\DevKit

4. 通过初始化来创建 config.yml 文件。在 `C:\DevKit` 文件夹内打开命令行窗口，输入下列命令：

	> ruby dk.rb init<br />
	> notepad config.yml

5. 在打开的记事本窗口中，于末尾添加新的一行 `- C:/Ruby23-x64`，保存文件并退出。

6. 回到命令行窗口内，审查（非必须）并安装。

	> ruby dk.rb review<br />
	> ruby dk.rb install

## 安装 Jekyll
{: #install-jekyll}

1. 确保 gem 已经正确安装

	> gem -v

	输出示例：

	> 2.6.8

2. 安装 Jekyll 和 [Bundler](http://bundler.io/) gems

	> gem install jekyll bundler

3. 确保 jekyll gem 已经正确安装

	> jekyll -v

    输出示例:

	> jekyll 3.3.1

4. 确保 bundler gem 已经正确安装

	> bundle -v

    输出示例:

	> Bundler version 1.13.7

## 启动 Jekyll
{: #start-jekyll}

按照官方的 [Jekyll 快速开始手册][Jekyll Quick-start guide]
的步骤， 一个新的 Jekyll 博客可以被建立并在 [localhost:4000](http://localhost:4000)浏览。

> jekyll new myblog<br />
> cd myblog<br />
> bundle exec jekyll serve

<a class="post-image" href="/assets/images/posts/2013-05-11-new-jekyll-3-site.png">
<img itemprop="image" data-src="/assets/images/posts/2013-05-11-new-jekyll-3-site.png" src="/assets/javascripts/unveil/loader.gif" alt="New Jekyll 3 Site" />
</a>

## 故障诊断
{: #troubleshooting}

1. 错误信息：

	   "ruby" is not recognized as an internal or external command, operable program or batch file.

	**可能原因**： 该程序可能未被正确地安装或未在 PATH 里设置成功。

	**尝试解法**： 确保程序已被正确安装。然后手动将其添加至 PATH，请参考如下步骤[^1]。

	> 1. 按住 Win 键再按下 Pause
	> 2. 点击 Advanced System Settings
	> 3. 点击 Environment Variables
	> 4. 将 `;C:\Ruby23-x64\bin` 添加至 Path 变量的末尾
	> 5. 重启命令行

2. 错误信息：

	   ERROR:  Error installing jekyll:
	   ERROR: Failed to build gem native extension.

	   "C:/Program Files/Ruby23-x64/bin/ruby.exe" extconf.rb

	   creating Makefile
	   make generating stemmer-x64-mingw32.def
	   compiling porter.c
	   ...
	   make install
	   /usr/bin/install -c -m 0755 stemmer.so C:/Program Files/Ruby/Ruby200-x64/lib/ruby/gems/2.0.0/gems/fast-stemmer-1.0.2/li
	   /usr/bin/install: target `Files/Ruby/Ruby200-x64/lib/ruby/gems/2.0.0/gems/fast-stemmer-1.0.2/lib' is not a directory
	   make: *** [install-so] Error 1

	**可能原因**： Ruby 被安装在含有空格的路径里。

	**尝试解法**： 重新安装 Ruby，这次请不要使用带有空格的路径，或者请直接选择使用默认路径。

3. 错误信息：

       New jekyll site installed in C:/Code/GitHub/blog.
        Dependency Error: Yikes! It looks like you don't have bundler or one of its dependencies installed. In order to use Jekyll as currently configured, you'll need to install this gem. The full error message from Ruby is: 'cannot load such file -- bundler' If you run into trouble, you can find helpful resources at http://jekyllrb.com/help/!
       jekyll 3.3.1 | Error:  bundler

     **可能原因**: Bundler gem 未被正确安装.

     **尝试解法**: 运行命令 `gem install bundler`

4. 错误信息：

	   Generating... Liquid Exception: No such file or directory - python c:/Ruby200-x64/lib/ruby/gems/2.0.0/gems/pygments.rb-0.4.2/lib/pygments/mentos.py in 2013-04-22-yizeng-hello-world.md

	**可能原因**： 如果你正在使用 Jekyll 2 和 Pygments， 这个错误很可能意味着 Pygments 未能被正确安装或是 PATH 设置尚未生效。

	**尝试解法**： 首先请确保 Pygments 已成功安装且 Python 的 PATH 设置正确未包含空格和最后多余的斜杠。
    然后重启命令行。如果依旧失败，请尝试注销并重新登录 Windows。
    甚至使用终极解法，重启电脑。

5. 错误信息：

	   Generating... Liquid Exception: No such file or directory - /bin/sh in _posts/2013-04-22-yizeng-hello-world.md

	**可能原因**： 与 pygments.rb 0.5.1/0.5.2 版本的兼容性问题。

	**尝试解法**： 将 pygments.rb gem 的版本从 0.5.1/0.5.2 降至 0.5.0。

	> gem uninstall pygments.rb \--version '=0.5.2'<br />
	> gem install pygments.rb \--version 0.5.0

6. 错误信息：

	   c:/Ruby200-x64/lib/ruby/2.0.0/rubygems/dependency.rb:296:in `to_specs': Could not find 'pygments.rb' (~> 0.4.2) - did find: [pygments.rb-0.5.0] (Gem::LoadError)
	   from c:/Ruby200-x64/lib/ruby/2.0.0/rubygems/specification.rb:1196:in `block in activate_dependencies'
	   from c:/Ruby200-x64/lib/ruby/2.0.0/rubygems/specification.rb:1185:in `each'
	   from c:/Ruby200-x64/lib/ruby/2.0.0/rubygems/specification.rb:1185:in `activate_dependencies'
	   from c:/Ruby200-x64/lib/ruby/2.0.0/rubygems/specification.rb:1167:in `activate'
	   from c:/Ruby200-x64/lib/ruby/2.0.0/rubygems/core_ext/kernel_gem.rb:48:in`gem'
	   from c:/Ruby200-x64/bin/jekyll:22:in `<main>'`

	**可能原因**：如错误信息所述，找不到 pygments.rb 0.4.2，仅找到 pygments.rb 0.5.0。 （此问题出现于此文初稿时的 Jekyll 版本，现版本应已修复）

	**尝试解法**： 将 pygments.rb gem 的版本降级至 0.4.2

	> gem uninstall pygments.rb \--version “=0.5.0”<br />
	> gem install pygments.rb \--version “=0.4.2”

7. 错误信息：

	   Generating... You are missing a library required for Markdown. Please run:
	   $ [sudo] gem install rdiscount
	   Conversion error: There was an error converting '_posts/2013-04-22-yizeng-hello-world.md/#excerpt'.

	   ERROR: YOUR SITE COULD NOT BE BUILT:
	      ------------------------------------
	      Missing dependency: rdiscount

	**可能原因**： 如果你还是在使用 Jekyll 2, 这个错误很可能是因为依赖包 `rdiscount` 未找到。
	此问题最有可能的原因是，网站使用的是 [rdiscount](https://github.com/davidfstr/RDiscount) 作为 Markdown 引擎，而不是 Jekyll 默认的引擎，故需要手动自行安装。

	**尝试解法**：运行 `gem install rdiscount`

8. 错误信息：

	   c:/Ruby200-x64/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:55:in `require': cannot load such file -- wdm (LoadError)
	   from c:/Ruby200-x64/lib/ruby/site_ruby/2.0.0/rubygems/core_ext/kernel_require.rb:55:in `require'
	   from c:/Ruby200-x64/lib/ruby/gems/2.0.0/gems/listen-1.3.1/lib/listen/adapter.rb:207:in `load_dependent_adapter'
	   from c:/Ruby200-x64/lib/ruby/gems/2.0.0/gems/listen-1.3.1/lib/listen/adapters/windows.rb:33:in `load_dependent_a
	   dapter'
	   ...

	**可能原因**： `wdm` gem 未被安装。因为 Jekyll 只官方地支持 *nix 系统，所以 [Windows Directory Monitor][WDM] 并没有作为依赖包而被自动安装。

	**尝试解法**：将 `gem 'wdm', '>= 0.1.0' if Gem.win_platform?` 加入 `Gemfile` 文件，然后再次运行 `bundle install`.

[Full installation instructions]: https://github.com/oneclick/rubyinstaller/wiki/Development-Kit#installation-instructions
[Jekyll Quick-start guide]: http://jekyllrb.com/docs/quickstart/
[WDM]: https://github.com/Maher4Ever/wdm

[^1]: <a href="http://stackoverflow.com/a/6318188/1177636">在 Windows 7 上添加 Python Path</a> by melhosseiny.