# Hugo零基础搭建上篇--Demo发布


## 0x00 前言

本篇教程仅针侧重点在于Hugo静态博客的本地环境搭建、本地demo创建和发布到GitHub Pages的一个过程，适合纯小白阅读。如果你主要想了解关于博客设计方面的问题，本篇对你几乎毫无帮助2333。我也是最近闲的发慌才开始捣腾静态博客这块，关于博客的装修设计问题自己也还在摸索，过段时间研究的差不多了再考虑写点相关的教程吧。

### Hugo博客的优点

既然市面上有那么多现成的博客平台，为什么要花时间去研究Hugo之类的静态博客呢，个人认为主要有两个优点：

+ 数据的安全：说到博客我就想起来已经挂掉的BlogBus，一声不吭说停服就停服，多少人的心血文章就这么没掉了，连个备份的机会都不给。所以对比与这些第三方博客平台，自己搭建博客最大的优点便是数据永远不会丢失。

+ 方便的样式客制化：大部分人都喜欢把博客改造成自己喜欢的风格，Hugo在这个方面做得其实和当年的QQ空间差不多，你只需稍微一丢丢的搜索能力和前端知识就可以完成大部分的样式改造。

### Hugo博客的缺点

Hugo的缺点也非常明显。首先就是搭建过程十分的劝退零计算机基础的朋友，看到代码就头疼完全不想继续操作。然后就是文章是用Markdown语法书写的，刚才开始的时候会有强烈的不适应感。


## 0x01 本地安装Hugo

### 下载Hugo

打开Hugo的GitHub项目地址 。  [点击传送](https://github.com/gohugoio/hugo/releases "超链接title")

![Hugo项目](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%281%29.png)

在页面中选择最上面的那个版本，点击hugo_版本号_Windows-32bit.zip  或者  hugo_版本号_Windows-64bit.zip进行下载，具体哪个看自己电脑的位数，现在基本都是64bit了。点击之后就会立刻开始下载，GitHub的下载速度有时候比较感人，耐心等等吧。

### 安装Hugo

打开我的电脑，在众多盘里面选择一个幸运盘打开，将Hugo安装进去，这里我选择了D盘。

在D盘新建文件夹，命名为**Hugo**，打开刚建好的Hugo文件夹，再新建两个文件夹，一个叫**bin**，另一个叫**Sites**。解压刚才下好的zip文件，里面有3个文件，把**hugo.exe**复制到刚建好的**bin**文件夹内，整个安装过程结束。

## 0x02 本地安装Git

如果你不知道什么是Git，emmm那就不要管那么多了，下就是了。

首先照例进入官网。[点击传送](https://git-scm.com/ "超链接title")

![git官网](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%282%29.png)

网页应该会自动识别你的系统和版本，直接点击页面中的  **Download 版本号 for 系统名**  下载就完事了。下载完成之后获得一个exe文件，双击打开，国际惯例除了指定安装目录之外无脑下一步就完事了。如果你非常在意细节，可以参考这篇文章。[点击传送](https://www.cnblogs.com/zzzxing/p/12515477.html "超链接title")

## 0x03 本地新建项目

### 新建项目

使用<kbd>Win</kbd>+<kbd>R</kbd>快捷键输入 ~~曹孟德~~ cmd后，进入命令提示符。当然如果你会用Git Bash的话，接下来的全部命令行操作用Git Bash也是可以的。输入

```CMD
d:
```

进入D盘，再输入	

```CMD
cd Hugo/Sites
```

进入刚刚创建好的**Sites**文件夹，现在开始创建博客项目。输入

```CMD
hugo new site mysite
```

没有出现错误的情况如下图所示

![创建项目](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%283%29.png)

其中**mysite**可以换成你想要起的任何英文名字，我这里用的名字是**blogtest**，回车之后便可以在**Sites**文件夹内看到我们刚刚创建好的项目文件夹，打开结构如下。

![主题目录](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%287%29.png)

### 安装主题

首先你需要去商城挑选一个主题。[点击传送](https://themes.gohugo.io/ "超链接title")

![主题详情页](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%284%29.png)

看中哪个主题就直接点击进入详情页，点击**Demo**可以查看案例，对案例感觉满意就返回，点击**Download**即可进入该主题的GitHub仓库，在浏览器地址栏把这个地址复制下来。

![git地址](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%285%29.png)

回到CMD，输入

```CMD
cd blogtest/themes
```

进入项目文件夹内的主题文件夹，开始准备安装一个自己喜欢的主题。输入

```CMD
git clone 你刚才复制的主题地址
```

![下载主题](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%286%29.png)

没啥意外等进度条走完就行了，GitHub有时候会抽风出现403，多试几次就好了23333。安装之后themes文件内就多了一个你刚刚下好的主题文件夹，之后对于主题的所有修改都在这个主题文件夹里面完成。

### 配置主题

打开主题文件夹，直接用搜索在里面找一个名为**config.toml**的文件，把它复制到你的博客项目的根目录下。

![搜索](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%288%29.png)

根目录下有一个同名文件，直接替换掉就好了。如果你不是很热衷于魔改的话，到这里关于主题的配置就结束了，如果你想进行一些客制化，可以自行百度，hugo的缺点就是文档缺的厉害，只能参考别人的经验自己一点点摸索了。这里提供一份参考：[点击传送](https://dp2px.com/2019/09/04/hugo-config/ "超链接title")

## 0x04 编辑文章

### 安装Typora

由于Hugo里面所有的文章都是Markdown语法写的，所以你需要一个趁手的Markdown编辑器，这里推荐使用Typora。

国际惯例打开官网。[点击传送](https://www.typora.io/#windows "超链接title")

选择符合你系统位数的安装包下载，如果嫌弃官网慢可以自行寻找第三方提供的安装包，下载完成后依旧打开无脑点击下一步即可。

### 创建第一篇文章

此时你的cmd应该在themes目录下，输入

```CMD
cd ..
```

返回到自己的博客根目录下，输入

```CMD
hugo new posts/first.md
```

![创建文章](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%289%29.png)

创建Markdown文件成功之后，你会在自己博客项目的根目录下的**content文件夹**中发现多了一个**posts文件夹**，你刚才创建的Markdown文件就在里面。这就是你的第一篇博文了，用Typora打开这个md文件，你就可以开始在里面编辑内容了。我们先随便写点东西在里面方便本次测试的时候看效果。

![md编写](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%2810%29.png)

这里有两点需要注意：

+ Markdown文件开头的  **draft: true**  这串字符表示你的这篇文章处于草稿状态，草稿状态下的文章是无法显示出来的，所以要将**true**改为**false**，才能将文章显示出来。

+ Markdown文件开头另起一行加入  **categories**  标签可以给文章增加分类，用于在博客中归类展示。格式如下：

  ```Null
  categories : [“分类名字”]
  ```

关于如何正确编辑Markdown的格式，建议参考这篇。[点击传送](https://www.jianshu.com/p/ebe52d2d468f "超链接title")

## 0x05 调试Hugo项目

### 正常情况

此时你的cmd应该在博客项目的根目录下，直接输入

```CMD
hugo server
```

![运行](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%2811%29.png)

回车之后如果没有报错，打开浏览器输入

```CMD
http://localhost:1313
```

即可进行对博客项目的本地预览，Hugo是支持实时更新的，所以你可以一边开着这个一边对主题文件进行魔改，方便实时查看变化。

想停止调试在cmd界面按<kbd>Ctrl</kbd>+<kbd>C</kbd>即可。

### 意外情况

极大部分情况是因为主题没有配置好的关系，建议详细阅读主题的安装文档，或者搜索使用同种主题的博主的文章进行解决。

## 0x06 发布博客

一般情况下Hugo发布是用的是GitHub Pages，当然你也可以托管到其他平台，这里以GitHub Pages为例。

### 创建GitHub项目仓库

如果你还没有GitHub的账户，当然是去注册一个。

国际惯例打开官网。[点击传送](https://github.com/ "超链接title")

![创建第一步](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%2812%29.png)

登录之后点击右上角的头像左边的小加号，点击**New repository**，进入创建仓库页面。其中**Repository name**这一项的建议写法为：

```null
GitHub用户名.github.io
```

![创建第二步](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%2813%29.png)

你的GitHub用户名就是左边**Owner**那栏里面的内容，然后权限选择**Public**，点击**Create repository**即可。

页面跳转进入新建好的仓库界面，记录下这个仓库的地址。

![创建第三步](http://q7l2ql4vs.bkt.clouddn.com/createhugo01-%20%2814%29.png)

### 上传项目

还记得前面安装的Git吗，接下来全靠它了。首先进入你的博客项目的根目录，在随便一个空白的地方点击右键，点击**Git Bash Here**进入Git的命令行窗口，输入

```git
hugo --theme=你的主题名字 --baseUrl="https://你刚才新建的github仓库的名字/" --buildDrafts
```

成功后直接在Git命令行窗口**依次**输入

```git
cd public
git init
git add .
git commit -m "备注信息，写点啥都行,不能不写"
git remote add origin 你刚才复制的仓库地址
git push -u origin master
```

一切顺利即可大功告成

### 在线访问博客

打开浏览器，输入**你刚才新建的GitHub仓库的名字**，即**GitHub用户名.github.io**便可以在线看到自己的博客了。

## 0x07 总结

一个Hugo的Demo上线基本就是这样一个流程，和普通的第三方博客平台进行对比，其实流程上都是有相似之处的。

+ 第三方博客注册帐号 = Hugo环境搭建 + 新建项目

+ 第三方博客选择主题 = Git工具安装 + 下载GitHub上的主题 + 配置主题

+ 在第三方博客网页上写文章 = 使用Typora写文章

+ 第三方博客发表文章 = Hugo静态页面生成 +  推送Hugo静态页面到GitHub仓库

+ 第三方博客提供的网址访问 = GitHub Pages提供的网址访问

在整个过程中，非要说有点困难的地方，那就是Hugo主题的适配，你需要去了解一些配置文件里面每一项的含义，相对应的将里面的内容进行替换。这一步确实对0计算机基础的小白有一些不太友好，不过现在大部分好看的主题在搜索引擎上基本都可以查阅到相应的配置教程，所以只要你有心思认真研究个一两天基本都是可以搭建出令自己满意的博客的。

下一篇文章将会简介给自己的Hugo博客更换域名、日常更新博客的操作流程和其他方面的一些小优化。
