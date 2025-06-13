---
toc_number: true
aplayer: null
copyright_author: null
copyright_info: null
copyright_author_href: null
copyright: null
toc: true
keywords: null
abbrlink: 32907
date: 2025-4-7 12:00:00 +0800
katex: null
title: 博客搭建(一)：Hexo博客搭建并部署自己的Butterfly主题
updated: 2025-06-13 19:06:00 +0800
description: hexo butterfly主题博客搭建方法
cover: null
top_img: null
categories: 经验总结
tags: 博客搭建
aside: true
comments: true
highlight_shrink: null
copyright_url: null
toc_style_simple: true
mathjax: null
---
# Hexo博客搭建

## 1. 前言

我不太习惯搭写博客，而且我学习速度也一般，属于不打破沙锅问到底，就学不会那种。
先说一下博客。博客在我看来就是个人网站。当然写博客比不写博客强，人总要留点东西出来，人生才有意义。
另一方面是给自己的学习知识，相关经验进行个整合：计算机网络，前端，以及可能的后端，以及python？
很多博客教程作者都喜欢写特别结构化的东西。冗余少，全是干货，看不懂的。
官方文档也是同样的，字典里都是干货，但没人喜欢啃字典。
我就用我的方式来写个教程了，也算是给自己做个总结。

## 2. 这是啥玩意

### 2.1 啥是hexo


Hexo是一个快速、简洁且高效的博客框架。
然后，为啥用Hexo？
因为这玩意用的人多，不想搞出选择综合征。去纠结哪个最好用不如选一个研究明白，然后其他的也好学了。
Hexo是个静态博客，相比python的django架构，这东西可以部署在github上。
而动态架构，你还需要个服务器在哪一直跑。
Hexo这边就是你随时得开着hexo server，这样你的每一次修改它都能马上给你响应，更新在网页上。
而且用的人多，东西丰富，教程多，美化好。
人生得意须尽欢，莫搞自己穷折腾。
框架的好处就是别人半个月的工程你一周内搞定。
别重复造轮子，你写出自己的博客，比学那些用不到的知识有用。


### 2.2 啥是butterfly


这是hexo的主题，也是个静态博客。
主题是可以自定义的，你可以自己写个主题，也可以用别人的主题。
我用的是butterfly主题，因为用的人多，且好看。


### 2.3 啥是github


当然，考虑到看着博客的教程人可能很多，我还是介绍下github。
github之于码农，好比知网之于大学生。
如果你是个爷们，那么github类似于贴吧，只不过是个代码吧，老哥些喜欢把自己捣鼓出来的东西扔这里。你也可以上传自己的东西。
如果你是个妹子，那么github又类似于小红书。只不过这里程序员为主，很多姐妹会分享自己的经验和代码，你可以上去查资料，问问题。当然，肯定和专门的论坛不一样。这里可没有什么绝绝子之类的东西，可能有些干活干麻了的掉头发四眼牢姐。
无论是贴吧，还是小红书，都有网盘的功能。你放上去的东东，大家就都能看。

下面是专业的。
github严肃的来说是个代码托管平台，你可以把你的代码上传到github上，然后别人可以下载你的代码。
当然，github也可以用来做博客。有个叫github page的存在，使得你可以把你的个人博客部署上去。
当然，国内还有其他类似的论坛和博客网站，如臭名昭著的csdn和半死不活的博客园。
但我还是建议你用github page，这玩意免费的，也有助于你的品牌形象。同时，这玩意没有广告，还是专门干活用的网站，和你没事撕逼的傻X也少。
而且，这里可以更自由些。


## 3. 开始

### 3.1 安装hexo


如果你要做饭，我建议你先搞个锅，灶台，炉子。
同理，安装hexo，
首先，你需要安装nodejs。
然后，你需要安装hexo。
安装nodejs可以去官网下载安装包，安装hexo可以用npm安装。

npm是啥，npm似乎是个包管理器。
就我踩得坑而言，这东西最好下好，很多配置你还需要用。
一般而言安装nodejs的时候，会自动安装npm。
如果没有，去官网下载安装包，安装npm。


### 3.2 搭建第一个hexo博客


很简单，搭建个空文件
在里面，打开cmd
或者打开git bash
输入 hexo init
文件生成完毕
输入 hexo clean 用于清空一堆之前生成的，不需要的静态文件
输入 hexo generate 用于生成最新更改内容的静态文件，这样才会显示出来
输入 hexo server 用于启动服务器，服务器会把这些静态文件渲染出来，这样你才能看到你的博客
打开浏览器，输入localhost:4000，你就可以看到你的博客了

当服务器启动后，你可以修改你的博客内容，保存后可以看到你的博客内容更新了。
有些不会更新，就需要你手动输入hexo clean和hexo generate，然后再输入hexo server，重复一遍之前的流程
你也可以用hexo server --debug，调试的话会有更多日志打印，帮助你理解hexo的工作流程。

最后，我们还需要把你的博客部署在github上，不然被人看个寂寞不是？
你需要修改配置文件，-config.yml，找到deploy，把它改为下面这样：
```
deploy:
    type: git
    repository: git@github.com:xxxxx/xxxx.github.io.git
    branch: xxxx
```
repository一般是你的github仓库地址.
branch一般是分支名，一般是main或者master

当然，你还需要在github上创建一个仓库，用于存放你的博客。
之后，输入 hexo deploy 用于部署你的博客。
部署成功后，你就可以在github page专用的网址上看到你的博客了。

好了，全文完。

总结下：
```
hexo init #初始化，生成一个模板
hexo clean #清空之前生成的静态文件
hexo generate #生成最新的静态文件
hexo server #(--debug) 启动(调试)服务器
hexo deploy #部署你的博客
```

碎碎念：
    需要注意，如果你先git clone下一个空文件仓，你是hexo init不了的。因为hexo init要创建个.git文件，与之冲突
    所以，建议先空文件，hexo init后，再把你的git挂上相关信息。
    真先clone后，要解决无法init也很简单，把.github删了，init之后重新连接远程仓库，重新部署
    deploy后会搞一个新git相关的文件，不用管它，跟你的要保存文件无关，只跟部署有关
    部署后的仓库中的文件和你的源码文件是不一样的，是两个东西！所以注意，版本管理别出问题了
    有的时候你的更新没显示在github page上，是因为github在验证你的提交，以及，浏览器缓存导致的
    所以，耐性等待，以及关闭浏览器，重新打开


### 3.3 安装butterfly，

一般而言，很多博主会使用npm来安装butterfly主题。
首先，你需要安装hexo。
然后，你需要安装butterfly。
这里把我在后面的总结挪了过来

```
npm install hexo-theme-butterfly
```

  这个指令对新手来说很坑，其文件下载后会安装在node_modules/hexo-theme-butterfly/_config.yml。你需要去修改这里面的配置文件，或者复制这个到根目录改名。具体操作我就不讲了，去node_modules依托里寻找主题还是难以接受

我这里推荐古法操作。由于我们以后肯定要魔改博客显示，butterfly主题不能更新就拉倒，我们可以放心这么玩。


├── themes/ # 主题目录（虽未显示但_config.yml中配置了主题

在项目中
```
git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```

这里的后缀， themes/Butterfly，就是让文件下载在命令行在当前目录下的这个路径

其中，master是稳定分支，dev则是实验性分支，这里肯定无脑推荐稳定分支。


-注意！

由于主题文件默认时不被git识别的，但我们可以使用git submodule来帮助我们同步主题仓库。

```
git submodule add https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly
```
使用这个指令，即可在推送再仓库后，同时跟踪子仓库，themes中的内容

如果你需要自己魔改内容，也可以自己fork，或者下载相关文件，新建一个自己的主题仓库，把链接换成自己的

这个指令执行后，git就会跟踪你的主题文件，同时会增加一个.gitmodules文件，里面的配置就是你的clone的仓库和部署路径

需要注意的是，如果用自己的仓库，建议使用https来克隆文件，使用ssh，就需要在netlify上找到depoly key，把这个注册到github你的仓库上，配置许可才行。


*

当我们下载好文件后，我们只改个文件就好啦

首先，要把旧的主题文件删了。原先根目录下有个_config.landscape.yml，我们这里把他改成_config.butterfly.yml

然后，到我们的butterfly主题文件中，把_config.yml 中的文件内容拷贝过来。

最后，我们在根目录的_config.yml中，找到并填上上theme: butterfly

我们的主题就搞好了
