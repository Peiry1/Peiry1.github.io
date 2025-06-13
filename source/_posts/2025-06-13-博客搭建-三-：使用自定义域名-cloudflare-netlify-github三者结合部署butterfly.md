---
layout: post
title: 博客搭建(三)：使用自定义域名--Cloudflare+Netlify+Github三者结合部署Butterfly
date: 2025-06-13 18:58:00 +0800
updated: 2025-06-13 18:58:00 +0800
categories:
  - 经验总结
tags:
  - 博客搭建
aside: true
comments: true
toc: true
toc_number: true
toc_style_simple: false
---


这里只需要简单的知道：

decap cms 必须依赖netlify托管，因为这是个动态的后台，不然会有netlify identify不通过的问题（无法登录）。

所以，本方案是使用github作为代码仓，使用Netlify进行网站构建和CMS管理，使用cloudflare进行自定义域名和dns管理，同时提供cdn加速。

上一节已经介绍了如何部署decap Cms。

本章节主要介绍三者联系，和如何整合三者。

\-

先说cloudflare。这绝对是个好东西.\
cloudflare上的域名是真的便宜，使用cloudflare购买的域名，结合cloudflare的域名托管，可以把第三方域名，折腾三天搞不定的各种麻烦是缩减到10min，然后你的代价就是一倍贵点的奶茶和咖啡。或者说，一个巨无霸套餐。换句话说，减少一次小资消费。\
实际上cloudflare也有cloudflare page。但我们已经把cloudflare 的域名用了，再搞一个构建是会与netlify的构建冲突的，而且不能用CMS了。我们的目标也是用这里的域名代理netlify的域名，就不做操作了。

\-

netilify也提供了免费域名，但是这个域名必须要有后缀netlify.app。你可以建立多个网站，在学习上和小型项目上是够用了。netlify的decap Cms已经在上一节介绍了。这里要提及的一天，就是netlify的identify git gateway，只要你跟自己的github仓库连接上了，就不用管了。生成的token key不用，且不能部署在github上的depoly key。它已经搞定了。

\-

github不介绍了。由于decap cms 绑定了netlify，github page 这里不可以用cloudflare的自定义域名，否则cms不可用。当然，由于github page 的部署是独立的，与netlify 的构建不互斥。

这里除了代码仓分支，还部署了另一个分支，专门用于存储代码仓在public中生成的静态文件，这样github.io域名也可以使用，且是独立的。

值得注意的是，如果你想用代码仓库进行构建，github默认的构建方式是基于jekyll的，这里不推荐使用。

最好的方式就是新建一个独立分子，单独管用于github page的depoly静态文件。

但是，这时访问xxx.github.io/admin，虽然会出现decap cms登录页面，用户是无法登录的。

可这里可以使用偷鸡做法，你可以强制域名访问重定向到netlify。只用修改decap cms的静态文件即可。

\-

理解上述操作后，下面说重点配置。

cloudflare上部署新域名，具体做法是先新增一个子域名。比如你买的域名是abc.uk（uk便宜），你就需要添加一些CNAME(C+NAME)类型的子域名，比如blog。这是，再把这个域名的代理写上你要代理的域名，这里是xxx.netlify.app，cloudflare就在dns上代理了这个域名，你访问blog.abc.uk，就相当于访问xxx.netlify.app。

当然，你也需要在Netlify上把你的自定义域名给配置好。由于这个域名不是在Netlify买的（贵的雅痞，抢钱！），Netlify需要你在dns那增加个说明文档，证明你娃头不是瞎搞，比如把别人域名给弄过来，搞大新闻。

这时候，就需要在cloudflare上新增一个txt类型代理，把netlify上生成的id和说明给写上去，证明你的域名真的是你的域名，不是张冠李戴。

完成之后，Netlify就知道，哦，这个域名也相当于访问我这个project，你就可以使用blog.abc.uk/admin 来访问你的cms了，愉快的进行博客编辑啦
