---
layout: blog
title: 使用hexo-next+LaTeX输入公式时遇到的一些错误
date: 2019年3月23日14:38:17
tags: LaTeX hexo-nex
categories: hexo
---

# 起因

去next配置里开了mathjax功能试了一下，遇到了些问题。

# 举个栗子

当你按照LaTeX语法在md文件里输入如下公式时，在本地的Markdown preview里是没有任何错误的，但是部署上线后会是如下的效果

<!--more-->

> 公式

```latex
$J(\theta)=-\frac{1}{m} \sum_{i=1}^{m}\left[y^{(i)} \log \left(h_{\theta}\left(x^{(i)}\right)\right)+\left(1-y^{(i)}\right) \log \left(1-h_{\theta}\left(x^{(i)}\right)\right)\right]$
```

> 效果

$J(\theta)=-\frac{1}{m} \sum_{i=1}^{m}\left[y^{(i)} \log \left(h_{\theta}\left(x^{(i)}\right)\right)+\left(1-y^{(i)}\right) \log \left(1-h_{\theta}\left(x^{(i)}\right)\right)\right]$

注意在`_`之间的部分全部被解析成了Markdown语法中的斜体，其实原因就是hexo在静态生成网页时是先用Markdown的语法解析器解析你的md文件，然后再交给mathjax解析其中的公式。

# 解决

在`_`前全部加上Markdown语法中的转义符`\`。

不过这样感觉就即不是纯正的Markdown，也不是是纯正的LaTeX了。

> 公式

```latex
$J(\theta)=-\frac{1}{m} \sum\_{i=1}^{m}\left[y^{(i)} \log \left(h\_{\theta}\left(x^{(i)}\right)\right)+\left(1-y^{(i)}\right) \log \left(1-h\_{\theta}\left(x^{(i)}\right)\right)\right]$
```

> 效果

$J(\theta)=-\frac{1}{m} \sum\_{i=1}^{m}\left[y^{(i)} \log \left(h\_{\theta}\left(x^{(i)}\right)\right)+\left(1-y^{(i)}\right) \log \left(1-h\_{\theta}\left(x^{(i)}\right)\right)\right]$