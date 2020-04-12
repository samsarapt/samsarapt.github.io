# 图片压缩的常见方式


## 0x01 压缩图片N个理由

### 云存储相关

现在的本地硬盘容量基本已经十分廉价了，但是云存储的费用还是有点小贵。压缩图片可以节约我们的云存储空间，以及减少每次加载图片时的流量，降低我们的费用支出。同时更小的图片可以加载的更快，提升用户体验。

如果你把自己的服务器当做图床的话，也会碰到这类问题。个人服务器的配置大多不高，带宽也就1M上下，主要都是用来加载css和js文件，基本不能有太多额外的图片消耗，压缩图片就能很好的解决这个问题。

### 第三方限制

现在许多的网站都对上传图片的大小有着严格的要求，如果你的图片大小超过规定上限将无法上传，需要将图片的大小进行压缩。

### 降低载体文件体积

如果图片时插入在word或者ppt中，大体积图片数量过多会引起整个文件的体积过大，不利于传输。

## 0x02 压缩图片的N种方式

### 利用聊天工具

将图片从一个QQ或者微信发送到另一个QQ或者微信，发送的时候不要勾选原图，然后接收，存储后，图片就已经是压缩后的了，占用空间极小。通过QQ空间将照片传入QQ相册也可以进行图片的压缩，非常适用于批量处理压缩图片。利用微信和QQ可以非常方便的压缩图片，但是有一个缺点，不能进行分辨率的调节，压缩率较高，较影响图片的质量。

### 使用在线网站

在线网站压缩的优点是方便快捷，无需安装随处可用，输入网址即可。缺点是文件体积限制、数量限制、隐私问题以及需要网络。下面推荐个人觉得比较优秀的几个站点：

+ [Optimizilla](https://imagecompressor.com/zh/)

一次可以批量压缩最多20张JPG或PNG图片，压缩完后还可以打包下载，该工具支持中文浏览，习惯中文界面的朋友不妨使用它，压缩完成后还可以调整图片质量，以及预览压缩后的图片。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-1.png)

+ [TinyPNG](https://tinypng.com/)

一次可以批量压缩最多20张JPG或PNG图片，压缩完后还可以打包下载，不过有时候服务器会抽风。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-2.png)

+ [Resize Photos](http://www.resize-photos.com/)

在压缩之前，你可以设置图片的宽度和质量，质量1到100，越小越不清晰。也支持设置格式JPG、PNG、GIF、BMP，压缩完之后还可以给图片增加效果，类似于美图秀秀那种一键美化图片的那种功能。缺点是访问速度有点慢。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-3.png)

+ [Docsmall](https://docsmall.com/image-compress)

支持JGP、PNG、批量压缩、打包下载，另外还有PDF压缩、PDF合并、PDF分割，功能比较丰富。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-4.png)

### 使用离线小工具

离线工具的优点是没有网络限制、数量限制和隐私问题。缺点个人觉得只有需要下载安装，不能随处使用。这里推荐两款工具。

+ [Imagine](https://github.com/meowtec/Imagine/releases)

支持PNG、JPEG、WEBP格式，支持批量，支持中文，界面简洁，压缩效果好，基本不失真。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-5.png)

+ [智图](https://zhitu.isux.us/index.php/preview/download)

智图是腾讯ISUX前端团队开发的一个专门用于图片压缩和图片格式转换的平台，其功能包括针对PNG，JPG，GIF等各类格式图片的压缩，以及为上传图片自动选择最优的图片格式。同时，智图平台还会为用户转换一份WEBP格式的图片。这个虽然也有网页版，不过还是推荐离线版。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-6.png)

### 使用Photoshop脚本

图片压缩也是图片处理的一部分，当然还是要cue一下图像处理界的重量级工具Photoshop。基础操作就是我们可以通过调整分辨率，图像格式等来进行图片压缩。这里重点介绍一个快捷方法，不仅可以大幅缩小图片体积，而且基本不失真。步骤非常简单：

首先，你要有一个已经安装好的Photoshop，用Photoshop打开需要压缩的图片，点击文件->导出->储存为web格式，或者直接使用快捷键<kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>Ctrl</kbd>+<kbd>S</kbd>。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-7.png)

根据原图的风格进行右边预设的选择。如果是超大的风景照片类，建议选择**低**。如果是截图类，建议选择**高**。自己对比一下四联图里哪个效果合适，点击选中，都不满意可以调节右边的品质后再选。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-8.png)

点击存储即可。下面对比一下，左边是原图3.87M，右边是压缩后648K。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-9.png)

放大7倍下查看，你会发现，体积缩小了到原图**16%**的情况下，看起来**基本没有区别**。虽然这张对比图也经过了压缩，不过大体就是这么个意思，不信你自己试试。这只是单个文件的处理，如果我们需要批量处理文件，可以写一个脚本来解决，也**非常简单**。首先，在点击窗口->动作，打开动作面板。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-10.png)

点击创建新动作按钮，给自己的动作起一个名字，点击记录。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-11.png)

创建完成后，图中红框内圆形图标为红色，说明正在录制动作。蓝框为停止录制，这个先记下来就好。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-12.png)

使用快捷键<kbd>Alt</kbd>+<kbd>Shift</kbd>+<kbd>Ctrl</kbd>+<kbd>S</kbd>，调出弹窗，选择对应的预设画质并保存。这里注意两点：

+ 保存的时候不要重命名，名字原来叫什么就是什么
+ 保存的路径就是之后每次使用这条脚本后，生成的文件的保存路径

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-13.png)

然后关掉这张图片的小窗（不是关掉整个ps软件），保存的时候原图文件名如果是中文会触发警告，无视就好。提示是否保存修改时选择**否**。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-14.png)

此时因为ps里没有打开任何一张图片，所有操作弹窗会消失。这时我们随便打开一张图，先把**动作操作栏**调出来，随后点击正方形按钮停止录制。再选中**打开**这条记录，点击垃圾桶图标进行删除。这样一个脚本就录制完成了。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-15.png)

接下来就是执行脚本，先把要处理的文件全部放在一个文件夹里。打开Photoshop，点击文件->自动->批处理。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-16.png)

在批处理弹窗中，选择你刚刚录制好的动作，选择你待处理图片所存放的文件夹，点击确定之前在下面核对一下待处理文件夹的路径是否手残点错了。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/2020-04-06-imgCompression-17.png)

然后你就可以去抽烟喝茶玩手机，基本上一秒一张的处理速度很快就处理完了，压缩完的文件都存放在你之前录制动作时的文件夹里，把第一张录制动作的图片删掉就大功告成啦。这个脚本是一次录制永久使用的，我一般会录制两个脚本，一个选择高预设，来处理截图，一个低预设，来处理风景照或者超大体积图片。这里附加说明一点，用来存压缩后图片的文件夹最好是固定给一个，不要删除，不然下次使用脚本的时候，要么在原路径重新新建一个同名文件夹，忘记名字的话只能重新录制脚本了23333
