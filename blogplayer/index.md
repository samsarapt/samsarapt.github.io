# 如何在博客中嵌入音/视频


## 0x01 &lt;iframe&gt;标签

&lt;iframe&gt;标签的作用是在一个html页面中，嵌入另一个html页面，说的通俗一点就是套娃，理论上用这个标签你可以将任何一个独立的页面嵌入到自己的页面中来。利用这个标签，我们可以非常轻松的将一些视音频网站提供的资源引用到自己的博客中来，目前大部分主流音乐、视频网站也都支持生成&lt;iframe&gt;标签的代码。

### 优点与缺点

优点只有一个，那就是简单方便好操作，无需自己上传源文件，点点鼠标复制粘贴即可。

缺点倒是有很多：

+ 有些歌曲、视频因为版权问题无法生成外链，这点在网易云特别严重
+ 因为跨域权限问题，我们无法修改播放器的样式，只能使用平台提供的样式，可能会和你博客的UI风格冲突，比如无法切换Light/Dark Mode
+ 因为一些众所周知的原因，无法加载YouTube、Vimeo等境外站点的资源
+ 引入的资源受到平台限制。bilibili限制了视频清晰度，只能引入360p画质，四舍五入等于不能看。国内其他主流视频平台清一色会先加载广告，体验极差
+ 资源可能会有被删除的风险

### 使用方法

音频以虾米音乐为例。打开虾米音乐官网，不需要登录。在搜索栏输入我们想要的歌曲，在搜索结果中选择你想要的那条记录，进入歌曲详情界面，点击立即播放。随后在下方的进度条区域，点击分享按钮。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-03-插入播放器-1.jpg)

在弹窗中点击**复制外链播放器代码**。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-03-插入播放器-2.jpg)

我们将获得以下代码。

```html
<iframe frameborder="no" 
        border="0" 
        marginwidth="0" 
        marginheight="0" 
        width="750" 
        height="110" 
        loading="lazy" 
        sandbox="allow-popups allow-scripts allow-same-origin" 	     		  
        src="https://www.xiami.com/webapp/embed-player?autoPlay=1&id=59454"
        >
</iframe>
```

将这段代码粘贴到你html页面中的相应位置即可完成嵌入。如果想在博文中嵌入，直接将这段代码复制到你的Markdown文件里即可。下面的全部代码同理，下文不再赘述。

视频以bilibili为例。进入对应的视频界面，点击图中红框的复制按钮后，将代码粘贴至所需位置即可。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-03-插入播放器-3.jpg)

其他平台的操作都大同小异，不是星际玩家应该都能顺利找到对应的外链分享按钮。不过一些平台的确是没有这个功能的，比如QQ音乐。

以及上述代码最好套在一个div里，自己写个css稍微控制一下样式，不然看起来还是会有点奇怪2333

### 效果展示

虾米音乐-demo：

<iframe frameborder="no" border="0" marginwidth="0" marginheight="0" width="100%" loading="lazy" sandbox="allow-popups allow-scripts allow-same-origin" src="https://www.xiami.com/webapp/embed-player?autoPlay=1&id=59454"></iframe>

bilibil-demo：

<div class="bilibili">
<iframe src="//player.bilibili.com/player.html?aid=285093269&bvid=BV1xc411h7uF&cid=171365567&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"> </iframe>
</div>



## 0x02 &lt;video&gt;标签

HTML5自带的视频播放器，可以实现一些基础的功能。

### 优点与缺点

优点：

+ 可以自定义样式，最大限度的保证了整个页面的美观
+ 保持原视频画质，没有广告污染
+ 可以播放你能下载或能访问到真实地址的一切资源
+ 支持画中画，即浮动视频窗口

缺点：

+ 需要自己下载资源并生成一个可供访问的外链，或找到别人生成的外链
+ 使用云存储的朋友可能要当心一下流量的问题
+ 功能和样式若想做的细致，需要引入一些第三方JS和CSS，操作繁琐，一般的小白改不来

### 基础使用方法

```html
<video autoplay
	   controls
	   height="1080"
	   width="1920"
	   loop
	   muted
	   poster="图片地址"
	   preload="none"
	   >
	<source src="mp4文件地址"  type="video/mp4">
  	<source src="ogg文件地址"  type="video/ogg">
  	<source src="webm文件地址"  type="video/WebM">
    在这里写文字，可以提示那些浏览器不支持此标签的用户。
  </video>
```

+ autoplay：自动播放，不要则不写
+ controls：显示进度条控制栏，不写不显示
+ height / width：播放器尺寸，可使用px、em、rem、百分百，建议写100%
+ loop：循环播放，不要则不写
+ muted：默认静音，不要则不写
+ poster：预览图片，类似于视频封面，不要则不写
+ preload：预加载，建议个人云存储用户别开，写none
+ mp4 / ogg / webm：三种视频格式，基本上只写mp4就好了
+ 如果强行引了一个音频的地址，视频播放器将变成下文的音频播放器，可以正常播放音频

### 进阶使用方法

如果对于默认的功能或样式有些不满意，可以使用一些第三方JS插件来进行修改，这里推荐Video.js，蛮不错的一个轮子，放出一点资料供大家参考。学海无涯，~~小白劝退~~就是干。

Video.js Demo下载。[点击传送](http://www.jq22.com/jquery-info404)

中文教程。[点击传送](https://www.cnblogs.com/afrog/p/6689179.html)

英文文档。[点击传送](https://docs.videojs.com/index.html)

常见问题。[点击传送](https://www.awaimai.com/2053.html)

### 基础效果展示

<video controls  preload="none"
width="100%"       poster="https://ss2.bdstatic.com/70cFvnSh_Q1YnxGkpoWK1HF6hhy/it/u=2470545752,1397828946&fm=26&gp=0.jpg">
	<source src="//q7l2ql4vs.bkt.clouddn.com/mp4demo.mp4"  type="video/mp4">
    在这里写文字，可以提示那些浏览器不支持此标签的用户。
  </video>





## 0x03 &lt;audio&gt;标签

HTML5自带的音频播放器，可以实现一些基础的功能。

优缺点与&lt;video&gt;标签大同小异，不再赘述,外加一点。

### 基础使用方法

```html
<audio autoplay
	   controls
	   loop
	   muted
	   preload
       width="500"
	   >
	<source src="mp3文件地址"  type="audio/mpeg">
    在这里写文字，可以提示那些浏览器不支持此标签的用户。
  </audio>
```

+ autoplay：自动播放，不要则不写
+ controls：显示进度条控制栏，不写不显示
+ width：播放器宽度。该标签设置height属性默认为54px，修改高度属性只会增加组件高度，肉眼可见的高度部分依旧为默认值
+ loop：循环播放，不要则不写
+ muted：默认静音，不要则不写
+ preload：预加载，建议个人云存储用户别开
+ 如果强行引了一个视频的地址，音频播放器将变成上文的视频播放器，可以正常播放视频

### 进阶使用方法

有Video.js，那自然有Audio.js，直接放链接。

Audio.js Demo 下载。[点击传送](http://www.jq22.com/jquery-info10248)

基础教程。[点击传送](https://www.cnblogs.com/q812717031/p/3427346.html)

官方文档。[点击传送](http://kolber.github.io/audiojs/)

### 基础效果展示

<audio controls preload>
	<source src="//q7l2ql4vs.bkt.clouddn.com/mp3demo.mp3"  type="audio/mpeg">
    在这里写文字，可以提示那些浏览器不支持此标签的用户。
  </audio>




## 0x04 Hugo博客shortcode

shortcode，翻译过来就是短代码，这并不是Hugo博客的专属，很多博客生成工具都有自己的一套shortcode，也支持自定义shortcode。我目前使用的这个主题，作者就自定义了许多shortcode，特别是音乐播放器个人觉得做的超棒。这里给一份文档，包含了原生自带的和本主题作者附加的，写的算是很全面，大家自行参考吧。[点击传送](https://hugoloveit.com/zh-cn/theme-documentation-shortcodes)

## 0x05 题外话

为了节约自己的云存储的空间，和尽量降低流量费用，音频视频这种大文件，能不放在自己的桶里就不放，所以我们尽量从别的网站那边抓取资源的真实地址。

在音频方面，推荐酷狗音乐、咪咕音乐，在前端很容易抓到资源地址，实在不会下个资源嗅探器即可，我上面效果展示中的资源用的全都是酷狗的23333。视频的话如果是MV之类的可以在酷狗抓到，如果是自己的视频的话，目前我也没啥好办法，暂时只能白嫖七牛云的每月10G桶了。

不过一般这种资源的地址都是没有SSL证书的，也就是链接是以http开头的。如果你的博客地址有SSL证书，你的地址就是以https开头的。这样就会发生在https页面中加载http资源的情况，也就是出现了混合内容，有非常大的概率http资源是加载不出来的。关于混合内容的问题我也没搞明白，我之前的主题是可以加载混合内容的，换了个主题就不行了emmmm，如果你也出现这种情况的话，那就只有两个选择：

+ 去掉博客域名的SSL证书，全站使用http加载
+ 把资源放到带有SSL证书的桶里，阿里七牛腾讯都可以

第一个方案的缺点就是浏览器会显示我们的网站为**不安全**，第二个方案的缺点就**贵**，大家自行斟酌吧，我是暂时把SSL证书停止解析了，等我研究出来上一个主题为什么能成功加载混合内容的时候再回来填坑。


