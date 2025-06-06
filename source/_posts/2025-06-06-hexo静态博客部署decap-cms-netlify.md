---
layout: blog
title: Hexo静态博客部署Decap CMS(Netlify)
date: 2025-06-06T18:02:00.000Z
thumbnail: /images/uploads/eqibxc2k-1200.avif
rating: 5
---
**这里是个标题**

好久没搞博客了，之前写的博客放在github page上就没碰了，导致现在想新搞一个CMS，一地鸡毛

不得已，还好之前及路过如何建立一个hexo博客（甚至没写完！）那就只好从头搞了

- - -

**先说下目标：**

我们要在已有的hexo架构的博客上，使用Netlify（net + life ->Netlify)静态博客后端管理，现在这个名字叫Decap CMS。

- - -

**那么，我们获得了什么？**

1通过这个Netlify，我们就能获得一个免费的域名, 后缀是xxxx.netlify.app（是的，你可以不再使用github page，多了个选择)。

2在这个域名上则绑定了我的github仓库，这意味着你还是可以通过github 来保管你的静态博客代码。

3更重要的是，Netlify 允许我们免费的使用其Decap CMS（前名：Netlify CMS)来管理我们的静态博客，这意味着我们可以像一些动态博客架构，比如python语言的django，来通过CMS，拥有一个admin后台来管理我们的博客。你就可以直接在网页上编辑管理你的博客，不用天天在本地编辑再，再用git push 推送到你的仓库啦！

4而且，通过CMS，你的修改会被Netlify 追踪，并同步到你的github仓库，你至此告别了git push。

- - -

我们的操作流程目录：

考虑到之前搞得一团糟，这里我们要从头开始，这样也能加深对前端的理解

1，新建一个hexo

    在本地选择一个位置，使用vscode打开，然后打开终端

    当然，可以用git bash，或者纯cmd，powershell，linux的terminal，mobaxterm都行

    这里假定你已经安装好了node.js，npm，hexo等等前置，我在上一post讲过

    然后输入hexo init

   hexo会给你生成一个全新的博客模板，一般而言在vscode上长这样。

   xxxx_project/
    ├──.github # GitHub相关配置目录（如workflows等）

    ├── node_modules/ # npm安装的依赖包目录
    ├── scaffolds/ # 文章模板目录（Hexo默认）
    ├── source/ # 源文件目录
    │ └── _posts/ # 博客文章目录

    ├── themes/ # 主题目录（虽未显示但_config.yml中配置了主题
    ├──_config.landscape.yml # Hexo主配置文件

    ├──_config.yml # Hexo主配置文件

    ├──.gitignore # Git忽略规则
    ├── package-lock.json # npm依赖锁定文件

    └──package.json # npm项目配置文件（虽未显示但应存在）

2生成静态文件

    在你执行完hexo clean 和hexo generate后，hexo就会给你生成一堆静态文件。
    这些静态文件在public目录下

    xxxx_project/
    ├──.github # GitHub相关配置目录（如workflows等）

    ├── node_modules/ # npm安装的依赖包目录

    **├──public/ # 生成的静态文件目录**
    ├── scaffolds/ # 文章模板目录（Hexo默认）
    ├── source/ # 源文件目录
    │ └── _posts/ # 博客文章目录

    ├── themes/ # 主题目录（虽未显示但_config.yml中配置了主题
    ├──_config.landscape.yml # Hexo主配置文件

    ├──_config.yml # Hexo主配置文件

    ├──.gitignore # Git忽略规则

    ├──db.json
    ├── package-lock.json # npm依赖锁定文件

    └──package.json # npm项目配置文件（虽未显示但应存在）

    当然，public中的具体内这里就不展开讲解了

    这时候你就可以使用hexo server，在本地上浏览你的博客会长什么样子了

3 github--饭桶之家

    如果我们想把我们的仓库同步到github上，我们该怎么做？

    当然，首先你要有个git，还要有个github账号
    vscode上在源代码管理上有把代码推上去的方法，你可以在图形界面操作，直接推上去

    但是，如果你网络没配置好，http推送就可能出问题！

    而且，大家一般而言更喜欢用ssh。

    所以，这里的操作如下。我实在vscode 终端新建了git bash来操作

    3.1首先，你要有个空的远程仓库。

        不管你是用图形界面，还是上github自己的账户来新建个仓库，都行

    3.2 git init !

        这个操作会在你的本地代码仓搞一个git来跟踪你的代码

    3.3 git remote

        如果你用图形界面，vscode会自动给你新建个仓库，然后把你的remote设置好

        但很可惜，你可能网络不好！或者没配置好，或者更喜欢ssh，就得手敲

        git remote -v会查看当前远程服务器是啥

        图形界面会给你设置成https，我们推荐ssh

        git remote remove origin 这一步会删去我们注册的的远程服务器

        git remote add origin git@github.com:xxxxxxxx.git 这里咱贴上我们的远程服务器名称即可

    3.4 git add .

        我建议这个操作前，先hexo clean，把public删了，那一堆静态文件我们后面再处理

        git add .是把当前目录下所有文件都扔进去，登记

        你也可以git add xxx，单独选择你要登记的文件

    3.5 git commit -m "xxxxx"

        这一步，我们就会给登记好的文件，加上登记条标签。comment就是评论嘛。

        一般而言大佳就会写我这次增加的文件是为了干啥

    3.6 git branch

        这一步存粹是检查你当前分支是啥。

        branch在英文里是树枝的意思。如果不能理解，主干道上的岔路就是branch。

        branch是管理你的代码分路的。如果你想给代码搞骚操作又不想影响整个代码，就可以开个新branch瞎搞，这样也不会影响主干。这个特别适合团队协作。

        好了，git branch 就是看你当前是啥分支
        git branch xxx会新建一个branch

        git branch checkout则会切换分支，switch那种

    3.7 git push!

        大费周章的提branch，就是为了不再这里被搞事情。

        git push origin xxxx(branch)

        这个指令就是把你的当前commit，推送到xxx这个branch上。

        origin是你的远程仓库，我们在3.3的remote里设置过了

        这里要确保的就是你当前的branch，和你要推上去的branch一致

        push 成功后，我们的github上就存放好了我们的博客代码

4搞个butterfly主题！

    一般而言，很多博主会使用npm来安装butterfly主题

       npm install hexo-theme-butterfly

    这个指令对新手来说很坑，其文件下载后会安装在node_modules/hexo-theme-butterfly/_config.yml。你需要去修改这里面的配置文件，或者复制这个到根目录改名。具体操作我就不讲了，去node_modules依托里寻找主题还是难以接受

\-

    我这里推荐古法操作。由于我们以后肯定要魔改博客显示，butterfly主题不能更新就拉倒，我们可以放心这么玩。

    ├── themes/ # 主题目录（虽未显示但_config.yml中配置了主题

    在项目中git clone -b master https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly

    这里的后缀， themes/Butterfly，就是让文件下载在命令行在当前目录下的这个路径

    其中，master是稳定分支，dev则是实验性分支，这里肯定无脑推荐稳定分支。

\-注意！

    由于主题文件默认时不被git识别的，但我们可以使用git submodule来帮助我们同步主题仓库。

    使用git submodule add https://github.com/jerryc127/hexo-theme-butterfly.git themes/butterfly，即可在推送同时跟踪themes中的内容

    如果你需要自己魔改内容，也可以自己fork，或者下载相关文件，新建一个自己的主题仓库，把链接换成自己的

    这个指令执行后，git就会跟踪你的主题文件，同时会增加一个.gitmodules文件，里面的配置就是你的clone的仓库和部署路径

    需要注意的是，如果用自己的仓库，建议使用https来克隆文件，使用ssh，就需要在netlify上找到depoly key，把这个注册到github你的仓库上，配置许可才行。

\-

当我们下载好文件后，我们只改个文件就好啦

首先，要把旧的主题文件删了。原先根目录下有个_config.landscape.yml，我们这里把他改成_config.butterfly.yml

然后，到我们的butterfly主题文件中，把_config.yml 中的文件内容拷贝过来。

最后，我们在根目录的_config.yml中，找到并填上上theme: butterfly

我们的主题就搞好了

5 把博客推到Netlify上！

    笔者这里在上传到netlify 进行depoly时，发现静态文件中的css一个没生成！但在本地是好的。在排查问题中取消了了使用submodule，改用全部跟踪Themes下的butterfly。这样也方便自己魔改文件。方法就是去掉butterfly文件中的.github文件。

    但最后发现原因是自己的文件名是themes/Butterfly，而_config.ymal中配置的的是butterfly。修正大小写后，netlify就depoly成功了。

    原因时netlify 网页上时linux后台，跟我们的Window系统和MacOS不一样，大小写敏感...

    被自己蠢到吐血。

- - -
