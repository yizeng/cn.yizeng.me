---
layout: post
title: "使用 Google Chrome 开发者工具审查和验证 XPath/CSS 选择器"
description: "本文演示了两种在不添加额外插件的前提下，使用 Google Chrome 开发者工具审查和验证 XPath/CSS 选择器的方法。
一种是直接在 'Elements' 面板内搜索, 另一种是在 'Console' 面板内使用 $x/$$ 命令。"
categories: [教程]
tags: [chrome, css selectors, selenium webdriver, xpath]
redirect_from:
  - /2014/03/23/
last_updated: 2017年5月30日
---

> 最近更新于 - 2017年5月30日

Google Chrome 浏览器自带了叫做 "[Chrome DevTools][Chrome DevTools]" 前端调试工具。
它包含一系列方便的调试工具，其中包括了在不添加额外插件的前提下，直接审查和验证 XPath/CSS 选择器的功能。

这可以通过如下两种方式完成：

- 使用 `Elements` 面板内的搜索功能来在 DOM 中审查验证并高亮 XPath/CSS 选择器。
- 在 `Console` 面板中执行命令 `$x("some_xpath")` 或 `$$("css-selectors")`来审查和验证。

## 通过 Elements 面板

1. 键入 `F12` 来开启 Chrome DevTools。
2. 默认设置下 `Elements` 面板将会自动打开。
3. 在当前面板下键入 `Ctrl` + `F` 来启用搜索模式。
4. 输入 XPath 或 CSS selectors 选择器来进行审查和验证。
5. 如果有任何元素被成功匹配，它们将会在 DOM 中以黄色高亮。<br />
   注意，如果任何字符串也被该 XPath 或 CSS selectors 选择器成功匹配，它们也将被认为是有效的搜索结果。
   比如，CSS 选择器 `header` 将会匹配 DOM 中（包含 CSS 和脚本）含有 `header` 的任何关键字，而不仅仅是页面的元素。

<a class="post-image" href="/assets/images/posts/2014-03-23-evaluate-using-elements-panel.gif">
<img itemprop="image" data-src="/assets/images/posts/2014-03-23-evaluate-using-elements-panel.gif" src="/assets/javascripts/unveil/loader.gif" alt="使用 'Elements' 面板的搜索功能来审查和验证 XPath/CSS 选择器" />
</a>

## 通过 Console 面板

1. 键入 `F12` 来开启 Chrome DevTools。
2. 切换至 `Console` 面板。
3. 输入 XPath 选择器，如  `$x(".//header")` 来进行审查和验证。
4. 输入 CSS 选择器，如 `$$("header")` 来进行审查和验证。
5. 检测命令运行结果
	- 如果有页面元素被成功匹配，它们将会被在一个列表中返回。否则，将返回一个空列表 `[]`。

	> $x(".//article")<br />
	> [&lt;article class="unit-article layout-post"&gt;...&lt;/article&gt;]
	>
	> $x(".//not-a-tag")<br />
	> [ ]

	- 如果 XPath 或者 CSS selector 不合法，一个异常将被抛出并以红字显示。例如：

	> $x(".//header/")<br />
	> SyntaxError: Failed to execute 'evaluate' on 'Document': The string './/header/' is not a valid XPath expression.
	>
	> $$("header[id=]")<br />
	> SyntaxError: Failed to execute 'querySelectorAll' on 'Document': 'header[id=]' is not a valid selector.

<a class="post-image" href="/assets/images/posts/2014-03-23-evaluate-using-console-panel.gif">
<img itemprop="image" data-src="/assets/images/posts/2014-03-23-evaluate-using-console-panel.gif" src="/assets/javascripts/unveil/loader.gif" alt="Evaluate XPath/CSS selectors using 'Console' panel" />
</a>

## 优点和缺点

一个方法的优点往往是另一个的缺点，或反之。

<div class="data-table">
<table>
<tbody>
<tr>
	<th>通过 Elements 面板</th>
	<th>通过 Console 面板</th>
</tr>
<tr class="center bold">
	<td>优点</td>
	<td>缺点</td>
</tr>
<tr>
	<td>简单，快速，易达</td>
	<td>需要切换至其面板</td>
</tr>
<tr>
	<td>结果直接在 DOM 内高亮显示</td>
	<td>结果现在在一个列表里<br />需要点击元素，并右键选择返回在 'Element' 面板显示</td>
</tr>
<tr>
	<td>显示了搜索结果数量</td>
	<td><del>只显示搜索结果列表</del><br />(最新版的开发者工具已能显示列表内元素数量)</td>
</tr>
<tr class="center bold">
	<td>缺点</td>
	<td>优点</td>
</tr>
<tr>
	<td>匹配的字符串也会被显示</td>
	<td>只会匹配页面元素</td>
</tr>
<tr>
	<td>只能审查，不能验证<br />不会对不正确不合法的选择器报错</td>
	<td>对不合法的选择器抛出异常</td>
</tr>
<tr>
	<td class="center">-</td>
	<td>可以在 Console 面板内直接使用其他功能</td>
</tr>
</tbody>
</table>
</div>

[Chrome DevTools]: https://developers.google.com/chrome-developer-tools/
