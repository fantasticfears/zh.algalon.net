---
title: Hexo 的不一致设计和优秀
tags:
  - Hexo
---

[Hexo][hexo] 是后起之秀。Hexo 是 JavaScript 的血亲。这又是这个世代的双城记。

## Good part

Hexo 基于 JavaScript，快速迭代，同时还有极好的性能。作为一个静态网页生成器，还能轻松部署到 GitHub Pages 以及国内的服务。这些都不用带来写任何代码的代价，对用户来说真是一个非常棒的选择。

Hexo 独立了主题，编辑的主题和内容的分离是很好的选择。更少的代码量，我不用去改动主题。作为一个白目用户，我不用去操心主题的改动，我只要用优雅的 [Next](https://github.com/iissnan/hexo-theme-next)[^next] 即可。
主题中也可以用 npm 的大量工具链，封装良好，容易检视和理解。毕竟所有能被 JavaScript 重写的代码，都会被 JavaScript 重写。

Hexo 也拥有众多选项，用简单的方式给用户极大的选择。同样很不幸的，这是无数 npm 包选项的意大利面式堆砌。

## :(

Hexo 无可避免地受到 Jekyll 的影响，从此灾难开始。Jekyll 所有下划线 `_` 开头的代表站点内容；`.`、`#`、`~` 是隐藏文件。这些文件不会被 build。Jekyll 会生成幂等的目录结构，目录原来是怎么样的，生成什么样的。所以 Jekyll 要遵循 convention。既然 Hexo 已经用 source 和 scaffolds 了，那么这下划线意义何在...Hexo 只关心自己需要的目录。

Hexo 学习了 npm 的生态，模块化，但是连 RSS 都拆出去是为了什么？要使用 RSS 的话会需要加入 `hexo-generator-feed` 模块。这意味着同时带来了 package.json，这个及其难以手动修改的库管理文件。对比之下，Bundler 确实设计良好……现在 Next 主题还没有替换掉被 deprecated 的 bower。

Hexo 的主题有独特的配置文件，这个配置文件不只是主题的默认配置。想要配置主题的功能，需要进到主题里去配置它……这一下就把隔离主题的意义毁了。gitmodule 跟踪了主题之后，仍然需要修改主题内容。另外 Hexo 没有实现覆盖文件的方法。同理配置文件的分离让数据源和 assets 出现在了两个位置，这真是太尴尬了。Don't Repeat Yourself.

Hexo 的主题可以很复杂，Hexo 没有阻止主题使用 Pipeline，那么对于 Next 这样的极高请求数的主题，甚至应该提供 pipeline 的机制来处理 assets。选择复杂还是简单，是一个 Hexo 还没有解答的问题。

hexo server -d 是什么东西，真有人静态网页不用 nginx 部署么？还不用说微妙的 cache 问题导致每次运行命令的时候都需要 hexo clean……

[hexo]: https://hexo.io/
[^next]: 博客站的载入特效没有意义，影响搜索引擎的过客找到重要的内容。
