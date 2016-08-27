---
layout:     post
title:      "GitHub Pages + Jekyll 搭建个人Blog "
subtitle:   "Blog搭建指南"
date:       2016-08-26 2:25:00
author:     "Skylark Yan"
header-img: "img/in-post/hello.jpg"
tags:
    - 技术
    - Jekyll
    - GitHub
    - GitHub Pages
    - Blog
---

> 在这篇文章开始之前，你最好已经安装了 [Git](https://git-scm.com/) 并了解了它的基本使用，如果对于 Git 的安装及使用还有疑问，推荐去看看[廖雪峰的 Git 教程](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)，方便之后的操作。另外这篇文章基于Windows环境，相信Linux使用者可以自行变通。

> PS：本篇文章的很多内容都是借鉴了[GitHub Help](https://help.github.com/)中的文档，大家可以去看看详细内容。另外文章部分内容也参照了P_Chou大大的这篇[Blog](http://www.pchou.info/ssgithubPage/2014-07-04-build-github-blog-page-08.html)，特此声明，以表感谢。

## 探索个人Blog的开端

我最早接触到用 [GitHub Pages](https://pages.github.com/) + [Jekyll](http://jekyllrb.com/) 搭建个人`Blog`是在今年3月的时候，那时候刚开始搞点前端的东西，和同学一起参与了[百度前端技术学院](http://ife.baidu.com/task/all)的任务，预热的任务就是利用`GitHub Pages`搭建一个`Blog`，虽然到后来那一堆任务由于时间和能力关系，没有完全完成提交，不过对搭建`Blog`的相关技术产生了兴趣，拖拖拉拉搞到现在总算是搞好了。

基本上我在搭建过程中整体参照了P_Chou大大的这篇[Blog](http://www.pchou.info/ssgithubPage/2014-07-04-build-github-blog-page-08.html) ，原文链接放在这里，大家可以去看看。

下面我就说说自己搭建`Blog`的过程和基本步骤，希望能够对别人有所帮助。

## 关于 GitHub Pages

### GitHub Pages

`GitHub Pages` 是一个免费的静态网站托管平台，由 `GitHub` 提供，它具有以下特点：

1. 免空间费，免流量费，省去了购买服务器的费用及麻烦；
2. 有个人用户或组织主页和项目主页两种选择；
3. 支持页面生成，可以使用 `Jekyll` 来布局页面，使用 `Markdown` 来书写正文；
4. 可以自定义域名。

### 个人用户或组织主页和项目主页

`GitHub` 有两种基本类型的 `GitHub` 主页：

* 个人用户或组织主页
* 项目主页

它们几乎是相同的，但它们之间有一些重要的区别。 

| `GitHub` 主页的类型  | 主页默认域名                      | 构建页面的源文件的位置                                      |
|:-------------------:|:--------------------------------:|:---------------------------------------------------------:|
| 个人用户主页         | `username.github.io`             | `master`分支                                              |
| 组织主页             | `orgname.github.io`              | `master`分支                                              |
| 个人用户的项目主页    | `username.github.io/projectname` | `master`、`gh-pages`分支，或者`master`分支中的`/docs`文件夹 |
| 组织账户的项目主页    | `orgname.github.io/projectname`  | `master`、`gh-pages`分支，或者`master`分支中的`/docs`文件夹 |

#### 个人用户或组织主页

对于个人用户主页来说：

* 你必须使用`username.github.io`命名你主页的仓库，比如我的`SkylarkYan.github.io`，并且这样命名的用于存放个人主页的仓库一个账户只能有一个，具有唯一性。
* 构建和发布你的`GitHub`主页的内容必须放在`master`分支中。
* 没有使用自定义域名的话，你可以通过`http://username.github.io`来访问你的主页。

对于组织的主页来说，同样的：

* 必须使用`orgname.github.io`命名主页的仓库。
* 构建和发布的`GitHub`主页的内容必须放在`master`分支中。
* 没有使用自定义域名可以通过`http://orgname.github.io`来访问主页。

#### 项目主页

与个人用户和组织的主页不同，项目主页和项目本身保存在同一个项目仓库中。个人账户和组织账户都可以创建项目主页。项目主页类似于个人用户或组织主页，但也有一些差别:

* 你可以从`master`或`gh-pages`分支构建和发布项目主页，或者你也可以用`master`分支中的`/docs`文件夹。
* 如果没有使用自定义域名,项目主页会在在用户主页的子路径：`username.github.io/projectname`，使用自定义域名则随域名变动。
* 个人账户的项目主页`URL`为`http://username.github.io/projectname`，而一个组织的项目主页`URL`为`http://orgname.github.io/projectname`。

以上就是关于个人用户或组织主页和项目主页相关内容的简介，详细的信息可以看看[GitHub官网的说明](https://help.github.com/articles/user-organization-and-project-pages/)。

一般来说搭建个人`Blog`用个人主页或者项目主页都是可以的，比如我参考的P_Chou大大的那篇教程就是用项目主页来做个人`Blog`的，而我自己则是用个人主页做`Blog`的，因为我觉得项目主页还是比较适合做每个项目的展示`Demo`之类的，个人`Blog`还是单独放一个专用仓库吧。在后面说明搭建`Blog`的流程中，我会以用个人主页搭建为主来说明，当然用项目主页的差别也不大，我也会顺带提一下。

## 关于Jekyll

`Jekyll`是什么?它实际上是一个模板转化引擎。它同时也是`GitHub`上的一个开源项目：[Jekyll](https://github.com/jekyll/jekyll)。

`Jekyll`本身基于`Ruby`，它实际上也可以看成是一种模板引擎`liquid`的扩展。`Jekyll`对`liquid`的主要扩展在于内建专用于博客网站的对象，可以在模板中引用这些对象：如`page`、`site`等，方便构建博客网站。

与其他的模板引擎一样，标记是模板引擎解析的关键，`liquid`设计了如下两种标记：

> PS：在这之后所有liquid引擎中的{ {、} }、{ %、% }标识，中间都是没有空格的，只是为了避免这些标识被解析，才加了空格，等找到解决方案之后我会改回去的，大家注意不要搞错了。

* `{ { … } }`：此标记表示的是将其中的变量转化成文本
* `{ % … % }`：此标记用于包含控制流关键字，比如：`{ % if % }`、`{ % for x in xx % }` 

显而易见的是，有了这种标记的支持，再加上`Jekyll`内建的对象，构建个人`Blog`就方便不少了。关于`Jekyll`还有在`GitHub Pages`中使用`Jekyll`的相关内容可以去[GitHub官网的帮助信息](https://help.github.com/articles/using-jekyll-as-a-static-site-generator-with-github-pages/)看看。

## 搭建个人Blog的具体步骤

前面balabala说了一大堆相关的东西，现在正式开始说明搭建`Blog`的过程和步骤。

### 创建Blog的GitHub项目仓库

这部分应该不用细说，只要你熟悉了`GitHub`的基础知识和基本操作，这一步应该没什么问题。我是用个人主页搭建`Blog`的，建立一个名为`username.github.io`的仓库，把相关文件放在`master`分支即可。若用项目主页，则按照之前项目主页的说明，把构建`Blog`的相关文件放在项目仓库对应的位置即可。

![](http://i.imgur.com/wI9Dpgn.png)

PS：图中示例不完全正确，我的`username`是`skylarkyan`，应该建立名为`skylarkyan.github.io`仓库，但是这个仓库是唯一的，已经存在了，所以不能创建，改了名字只起示例作用。

### 搭建本地环境

第一步，搭建本地测试环境，这一步虽然理论上不是必须的，但是我觉得基本就是必须要做的。因为之前我搭建`Blog`的时候刚开始本地环境没有搭建好，就想先跳过这一块，结果就是每改动一点内容我都需要`push`到`GitHub`上才能看到效果，整体效率就变的特别低，还是不要作死了= = ，乖乖把本地环境搭建好吧，毕竟也挺简单的。

#### Ruby和RubyDevKit的安装

前面说过`Jekyll`是基于`Ruby`开发的，因此想要在本地搭建一个测试环境需要`Ruby`的开发和运行环境。附上[Ruby的下载地址](http://rubyinstaller.org/downloads/)。`Windows`还是无脑安装，不断下一步下一步，不过记得安装过程中勾选添加`Ruby`到`PATH`系统环境变量，方便后面操作。安装完成后打开`cmd`输入`ruby --version`命令测试，输出`Ruby`版本号即安装成功。

```
$ ruby --version
ruby 2.2.4p230 (2015-12-16 revision 53155) [x64-mingw32]
```

还有`DevKit`，也从上面的链接下载，注意版本要与`Ruby`版本一致。下载下来的文件可以用`7-zip`解压，直接双击它会自解压到你选择的目录，解压完成后用`cmd`或`Git Bash`进入到刚才解压的目录下，运行下面命令：

```
$ ruby dk.rb init
$ ruby dk.rb install
```

命令执行完成后即`DevKit`安装完成。

#### Bundle安装

1.打开`cmd`或者`Git Bash`，输入命令`gem install bundler`并执行。

2.在根目录下创建一个名为`Gemfile`的文件，注意没有后缀名，用文本编辑器如`Sublime Text`添加下面内容到`Gemfile`中：

```
source 'https://rubygems.org'
gem 'github-pages', group: :jekyll_plugins
```

上面的链接是在国外的，得益于天朝的网络管理制度，即使翻墙了速度也不太理想。当然你不嫌慢多等会也可以用上面这个链接，反正我当时等了二十多分钟才完成（一脸黑线）。可以换成国内的[镜像链接](https://ruby.taobao.org/)，把`Gemfile`的内容改为：

```
source 'https://ruby.taobao.org/'
gem 'github-pages', group: :jekyll_plugins
```

3.输入命令`bundle install`并执行。命令会根据当前目录下的`Gemfile`，安装需要的所有组件。并且以后可以使用命令`bundle update`随时更新环境，保证正常使用。

```
$ bundle install
Fetching gem metadata from https://rubygems.org/............
Fetching version metadata from https://rubygems.org/...
Fetching dependency metadata from https://rubygems.org/..
Resolving dependencies...
```

4.输入命令`bundle exec jekyll serve`并执行，显示类似如下信息：

```
$ bundle exec jekyll serve
Configuration file: C:/git/SkylarkYan.github.io/_config.yml
        Source: C:/git/SkylarkYan.github.io
    Destination: C:/git/SkylarkYan.github.io/_site
Incremental build: disabled. Enable with --incremental
    Generating...
                done in 0.368 seconds.
Please add the following to your Gemfile to avoid polling for changes:
    gem 'wdm', '>= 0.1.0' if Gem.win_platform?
Auto-regeneration: enabled for 'C:/git/SkylarkYan.github.io'
Configuration file: C:/git/SkylarkYan.github.io/_config.yml
    Server address: http://127.0.0.1:4000/
Server running... press ctrl-c to stop.
```

然后访问 `http://127.0.0.1:4000/` 就可以看看本地测试环境的效果了，当然如果你的仓库为空肯定是404了，要在后面的操作完成后才会有页面显示。

### 在本地仓库编写Blog

在本地创建和`Github`上仓库同名的`username.github.io`文件夹，并在该目录下使用`Git Bash`执行`git init`命令，初始化本地仓库。若使用项目主页则与项目仓库保持同名，并在之后把相关内容文件放在合适的位置。

#### 符合Jekyll要求的网站目录结构

我们搭建`Blog`是基于`Jekyll`模板转化引擎的，`Jekyll`是专用于构建静态网页的程序。而想要`Jekyll`正常工作，就要让你的网站目录结构符合它的要求。更多关于`Jekyll`及其如何工作请看[这里](http://jekyllbootstrap.com/lessons/jekyll-introduction.html)。

在本地创建如下文件及文件夹，最终形成这样的目录结构：

```
-- username.github.io/
  ├- _includes/   
  │   ├- header.html
  │   └- footer.html
  ├- _layouts/   
  │   ├- default.html
  │   └- post.html
  ├- _posts/ 
  │   ├- 2011-10-25-open-source-is-good.markdown
  │   └- 2011-04-26-hello-world.markdown 
  ├- _site/  
  ├- assets/
  │   ├- img/
  │   ├- css/
  │   └- js/    
  ├- index.html    
  └- _config.yml 
```

各个文件及文件夹的解释：

* `_includes/` ：该目录下的文件可以用来作为公共的内容被其他文章引用。
* `_layouts/` ：该目录下的文件将作为主要的模板文件。
* `_posts/` ：博客文章应放在这个目录下，但需要注意，文章的文件名必须是`YYYY-MM-DD-Title.markdown`
* `_site/` ：这是启动Jekyll后生成的静态网页存放的地方。
* `assets/` ：这个目录没有强制的要求，主要是存放你的资源文件，图片、样式表、脚本等，你也可以在外层目录下存放这些文件。
* `index.html` ：默认的主页。
* `_config.yml` ：保存配置，该配置将影响`Jekyll`构造网站的各种行为。

#### 简单的编写Blog（一个例子）

这里参照P_Chou大大的[例子讲解](http://www.pchou.info/ssgithubPage/2013-01-07-build-github-blog-page-05.html)，通过完成一个例子快速的理解整个`Blog`的搭建。

对于基于静态页面的网站，你显然不希望每篇文章都要写`html`、`head`等与文章本身无关的重复的东西，那么容易想到的是将这些东西作为模板提取出来，以便复用，这也是`Jekyll`的作用。

`_layouts/`目录下的文件可以作为这样的模板。现在我们在`_layouts/`文件夹中创建一个模板文件 `default.html`：

```
<html>
   <head>
       <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
       <title>My blog</title>
   </head>
   <body>
   { { content } }
   </body>
<html>
```

`default.html`包含了每个`html`都需要的一些标记，以及一个个`liquid`标记。`{ { … } }`是`liquid`中用来表示“内容”的标记，其中的对象在解析时会被替换成文件到页面中。`content`：表示在这里的地方用子页面的内容替换。

现在我们来实现一个简单的主页，在仓库根目录下，创建一个`index.html`：

```
---
layout: default
---
<h1>Hello jekyll</h1>
<p>This is the index page</p>
```

除了普通的`html`标记外，开头这一段称为[`YAML`格式](https://github.com/jekyll/jekyll/wiki/YAML-Front-Matter)，以一行`---`开头，一行`---`结尾，在虚线的中间以`key-value`的形式对一些全局变量进行赋值。

`layout`变量的值表示该文章应当使用`_layouts/default`这个文件作为父模板，并将`index.html`中的内容替换父模板中的`{ { content } }`标记。

在根目录中启动`jekyll serve`（在`Git Bash`中执行`bundle exec jekyll serve`命令），并访问 `http://127.0.0.1:4000/index.html` ，你将看到如下页面：

![](http://www.pchou.info/assets/img/build-github-blog-page-05-img0.png)

该页面的`html`源码如下，可以看到，`index.html`中的内容替换了`default.html`中的`{ { content } }`

```
<html>
  <head>
      <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
      <title>My blog</title>
  </head>
  <body>
  <h1>Hello jekyll</h1>
<p>This is the index page</p>
  </body>
<html>
```

现在请观察一下`_site/`中的`index.html`，就是上面的`html`代码。现在你明白`Jekyll`的工作方式了吧，它仅仅完成一次性的静态页面的转化，其余的事情全都交给普通的`web server`了。

PS：请确保你的文件都是`UTF-8 without BOM`的编码。

> 在`windows`中，为了甄别`UTF-8`编码格式的文本文件，默认会在文件头插入三个字节的标识，被称为`BOM`。事实证明这是个“歪门邪道”，`Jekyll`不识别这种特殊的标记，所以可以使用`sublime text`等文本编辑器将`UTF-8`编码文件开头的`BOM`去掉。

现在我们来创建一篇博客文章，并在`index.html`页面添加文章的链接。

在 `_posts/`目录下创建`2012-01-07-first-post.html`

```
---
layout: default
title: my first post
---
<h1>{ { page.title } }</h1>
<p>This is my first post.Click the link below to go back to index:</p>
<a href="{ { site.baseurl } }/index.html">Go back</a>
```

修改`index.html`：

```
---
layout: default
---
<h1>Hello jekyll</h1>
<p>This is the index page</p>
<p>My post list:</p>
<ul>
   { % for post in site.posts % }
       <li><a href="{ { site.baseurl } } { { post.url } }">{ { post.title } }</a></li>
   { % endfor % }
</ul>
```

最终效果如下：

![](http://www.pchou.info/assets/img/build-github-blog-page-05-img1.png)

这里涉及到两个主要的对象:

* `site`：全局站点对象。比如`site.posts`返回当前站点所有在`_post/`目录下的文章，上面的例子结合`for`循环来罗列所有的文章
* `page`：文章对象。比如`page.url`将返回`page`对象的`url`，上面的例子用该对象和属性返回了文章的链接

    PS：`site.baseurl`的值就是我们在`_config.yml`中配置的`baseurl`。

这些对象被称为“模板数据API”，更多`API`文档请[参见这里](http://jekyllbootstrap.com/api/template-data-api.html)。

再提一下`liquid`，`liquid`是`Jekyll`底层用于解析的引擎，我们用到的`{ { … } }`亦或是`{ % … % }`标记其实是靠`liquid`去解析的。下面简单介绍下`liquid`的使用。

`liquid`包含两种标记，理解他们的机理是十分重要的：

* `{ { … } }`：输入标记，其中的内容将被文本输出
* `{ % … % }`：操作标记，通常包含控制流代码，例如：
    ```
    { % if user.age > 18 % }
        Login here
    { % else % }
        Sorry, you are too young
    { % endif % }

    { % for item in array % }
        { { item } }
    { % endfor % }
    ```

另外`liquid`还包含一种叫`filter`的机制。这是种对输出标记的扩展，通过它可以对输出标记中的内容进行更细致的处理，例如：

```
Hello { { 'tobi' | upcase } }
Hello tobi has { { 'tobi' | size } } letters!
Hello { { 'now' | date: "%Y %h" } }
```

对应的：

* 返回字符串大写的结果：TOBI
* 返回字符串的长度：4
* 将当前时间格式化输出

`liquid`内置了一些`filter`，并且该机制可以被扩展，`Jekyll`便扩展了`liquid`的`filter`。

> 更多关于`liquid`的使用方法，请[参见这里](https://github.com/Shopify/liquid/wiki/Liquid-for-Designers)；

> 更多关于`Jekyll`对`liquid`的扩展，请[参见这里](https://github.com/jekyll/jekyll/wiki/Liquid-Extensions)。

#### 使用Jekyll模板

通过上面的例子，我们明白了`Jekyll`的工作机制，以及具体如何去编写自己的`Blog`页面。当然你可以完全靠自己一个一个页面去写，但如果觉得麻烦的话，也可以使用现有的`Jekyll`模板，在模板的基础上进行修改。[现有的Jekyll模板](http://jekyllthemes.org/)

选择一个你喜欢的模板，然后把它`Download`下来，解压到你的本地仓库，或者直接把模板项目`clone`下来，放在你的本地仓库，再启动`Jekyll`本地测试环境，确认可用后，就可以在这个模板上进行修改，编写你自己的`Blog`了。

模板只是为我们搭建`Blog`提供了一个捷径，但很多内容还需要我们自己进一步修改，这里就不再详细说了，毕竟视每个人的情况都有所不同，就留给大家自己探索吧。

### 把本地项目push到GitHub仓库

假设你现在已经使用模板完成了自己`Blog`的搭建，但你目前只能在本地启动测试环境查看自己的`Blog`，这显然不是我们的最终目的，毕竟辛辛苦苦搭建一个`Blog`也是想拿出去给别人看看装装X的，只能自己写自己看当然对自己好处也很多，但还是少了点东西吧。所以我们现在要做的就是把本地的`Blog`项目`push`到对应的`GitHub`个人主页仓库`master`分支上。当然这里的前提是我使用的是个人主页，对应的就是`username.github.io`仓库的`master`分支。如果使用项目主页，同样参照之前的区别，把本地`Blog`项目`push`到对应的位置即可。

具体的操作，打开`Git Bash`，分别输入执行以下命令：

```
// 将当前的改动暂存在本地仓库
$ git add --all
// 将暂存的改动提交到本地仓库，并写入本次提交的注释是”first post“
$ git commit -m "first post"
// 推送master分支，该命令将会将本地master分支推送到github的远程仓库
$ git push origin master
```

相信熟悉`Git`基础知识和基本操作的你应该很熟悉这些操作。完成这些之后，我们就把本地的`Blog`项目`push`到了`GitHub`对应的仓库。这之后就可以尝试访问`https://username.github.io`进入自己搭建的`Blog`了。如果你使用的是项目主页，则访问`https://username.github.io/projectname`进入。

另外无论`Blog`生成失败还是成功，`Github`都会向你的邮箱发送一封邮件说明，请注意查收。

到这里我们的个人`Blog`就搭建完成了，中间可能还有一些小问题，相信大家可以自行解决，希望大家玩的开心！

## 个人Blog的高级玩法

### 分类和标签功能

分类和标签功能是`Jekyll`的`yaml-format`的内置功能，在每篇文章上方可以设置：这里需要注意的是如果多个分类或者`tag`的话，分开注明即可。分类可以任意添加，`Jekyll`在解析网站的时候会统计所有的分类，并放到`site.tags`中；换句话说，不能脱离文章而设置分类。比如这篇文章的头就有如下信息：

```
---
layout:     post
title:      "GitHub Pages + Jekyll 搭建个人Blog "
subtitle:   "Blog搭建指南"
date:       2016-08-24 16:00:00
author:     "Skylark Yan"
header-img: "img/in-post/hello.jpg"
tags:
    - 技术
    - Jekyll
    - GitHub
    - Blog
---
```

其中的`tag`就有四个，即四个标签分类，我的`Blog`中列出标签分类的代码如下，也是很简单明了的：

```
<div id='tag_cloud' class="tags">
    { % for tag in site.tags % }
    <a href="#{ { tag[0] } }" title="{ { tag[0] } }" rel="{ { tag[1].size } }">{ { tag[0] } }</a>
    { % endfor % }
</div>
```

其中也是用到了`liquid`引擎，大家也可以自己写处理`tag`的代码。

### 为Blog添加评论分享功能

其实这个或许都不能算是高级功能，`Blog`有评论分享功能应该是再正常不过了吧= =。但还是放在这里吧，没有太大问题……

我们自己去编写评论分享功能就太麻烦了，网上有很多评论分享插件，比如最早的`DISCUQ`、多说、友言等等。我这里使用了[多说](http://duoshuo.com/)的评论分享插件。

这些评论分享插件都是很好用的，并且基本都有非常完善的开发者文档说明供我们查阅。比如我使用的多说，就提供了完整的[开发文档](http://dev.duoshuo.com/docs/)，基本只需要把它提供的通用代码放到自己的页面里，并按照开发文档简单配置好就可以了。你可以在我这篇文档的最下方查看多说评论分享插件的效果。

多说还提供了评论管理等后台功能，总体上完全可以满足我们的需求，大家快自己动手尝试一下吧。

### 自定义域名的使用

目前我的域名备案还没有完成，所以还没有尝试使用自定义域名。这部分在网上可以找到很多教程，大家可以先看看，我把这部分先留空了，之后自己试过了再改吧。

## 写在最后

这篇博文我是真的写了好久= =，但还是感觉有些地方不完善，之后再继续改进吧。果然自己再写一遍就有很多东西捋清楚了，以后还是要多写点技术方面的东西吧。就先到这里了，拜~