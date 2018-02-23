---
layout: post
title: Gitalk初始化报错"validation failed"
subtitle: 记录总结评论插件初始化错误
date: 2018-02-22 T00:00:00.000Z
author: 高国峰
header-img: img/post-bg-debug.png
catalog: true
tags:
  - github
  - blog
  - gitalk
  - 解决问题
---

# 简介
在[《为博客添加 Gitalk 评论插件》](https://ggfocus.github.io/2017/12/19/%E4%B8%BA%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0-Gitalk-%E8%AF%84%E8%AE%BA%E6%8F%92%E4%BB%B6/)此文里已写的很详尽了，此处不再赘述。那一篇博客也是引用另一位哥们的，模板也是直接引用，文章已标明作者，在此表示感谢之情。本篇主要是分享在安装插件的过程中遇到的问题及解决之道。

## 问题1--Issues are disabled for this repo
### 问题描述
* 页面打开时，Gitalk插件进行初始化时，报错“Error: Issues are disabled for this repo”


### 分析及解决方案
谈到该问题出现的原因主要涉及Gitalk的工作原理--Gitalk 是一个基于 Github Issue 和 Preact 开发的评论插件。而原来我的项目是直接从前面那位哥们的GitHub上直接fork下来的，引用的依然是他的issue。因为fork的项目并没有自己独立的issue。repo应该是repository的缩写，故该报错即为此仓库的issue是不可用的。解决办法是重新建一个空白项目，把代码移过去。如果没有域名可以建一个项目过渡gaoguofeng.github.io，然后把现在的项目直接删掉，重新建一个同名的项目，例如GGFocus.github.io,可以直接用地址导入。

## 问题2--#422 Error: Validation Failed
### 问题描述
* 页面打开时，Gitalk插件进行初始化时，报错“Error: Validation Failed”


### 分析及解决方案
此问题和配置的ID长度有关，ID太长，导致初始化失败。如下：

``` HTML
  <!--Gitalk评论start  -->
  {% if site.gitalk.enable %}
  <!-- 引入Gitalk评论插件  -->
  <link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
  <script src="https://unpkg.com/gitalk@latest/dist/gitalk.min.js"></script>
  <div id="gitalk-container"></div>
  <script type="text/javascript">
      var gitalk = new Gitalk({
      clientID: '{{site.gitalk.clientID}}',
      clientSecret: '{{site.gitalk.clientSecret}}',
      repo: '{{site.gitalk.repo}}',
      owner: '{{site.gitalk.owner}}',
      admin: ['{{site.gitalk.admin}}'],
      distractionFreeMode: {{site.gitalk.distractionFreeMode}},
      id: window.location.pathname,
      });
      gitalk.render('gitalk-container');
  </script>
  {% endif %}
  <!-- Gitalk end -->
```

把ID改短一点，修改后为：



![](https://github.com/GGFocus/GGFocus.github.io/blob/master/img/home-bg.jpg)




此代码在_layouts文件夹中的post.html中,修改后刷新即可。
