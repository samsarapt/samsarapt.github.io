# Python-自动生成每日海报


## 0x00 前言

一个小伙伴说他需要帮一个品牌做每日海报，就是把一张背景图加上当日的时间信息、品牌信息和一句每日语录再导出，天天用PS作图很烦躁，问我有没有简单点的办法。接到这种奇奇怪怪的需求自然是能激起我的创造欲望的，故决定写一个自动生成海报的脚本来解决这个问题。

## 0x01 基本需求分析

海报的样式如下。鉴于不透露客户的信息，我稍微替换了一下内容。

![](https://ptbuff-1301738307.cos.ap-guangzhou.myqcloud.com/snipaste_20200428_220539.png)

可以看出脚本功能上的基本需求如下：

+ 通用于MacOS和Windows系统
+ 获取当日的英文月份、数字月份。日期、英文星期信息、中文星期信息
+ 输入一句每日语录
+ 语录后的黑色蒙版长度需根据语录长度自适应
+ 字体的样式指定，如大小、字体、位置等
+ 保证日期信息的排版样式
+ PNG图片的嵌入，如顶部LOGO、中间语录背后的黑色蒙版、底部的slogan图片、底部的地址信息

## 0x02 开发环境分析

### 环境选择

根据上面的需求分析，基本是一个简单的图片处理问题，可以采用的语言有很多，例如：Java、C#、JS等。综合考量下来，决定采用Python开发，理由如下：

+ Windows安装简单，可以自动配置环境变量
+ MacOS自带Python2环境，安装Python3也十分方便
+ 本地运行无需联网，不需要额外的服务器等配置

### 环境配置

+ 安装Python3环境
+ 安装Pillow库

## 0x03 需求实现

### PNG图片嵌入

利用Python的Pillow库可以轻松实现这一点，这里以添加LOGO图片为例

```python
#设置原图路径、logo路径
bgImageFile = "." + os.sep + "Img" + os.sep + "demo1.jpg" # 原图路径
logoImageFile = "." + os.sep + "Img" + os.sep + "logo.png" # logo图路径

# 调整logo大小
logoScale = 1  # 缩放倍数，大于1为放大，小于1位缩小，等于1为不变
logoWidth = int(logoImage.size[0]*logoScale)  # 设置缩放宽度
logoHeight = int(logoImage.size[1]*logoScale)  # 设置缩放长度
logoImage = logoImage.resize((logoWidth, logoHeight), Image.ANTIALIAS)  #整体缩放logo图片

# logo坐标
logoLocationX = 2350 # 横坐标
logoLocationY = 150  # 纵坐标

# 绘制logo
r,g,b,a = logoImage.split()  # 将色域分离，不做这一步png的透明背景将变成黑色
bgImage.paste(logoImage, (logoLocationX,logoLocationY), mask=a)  # 放置logo图片
```

中间语录背后的黑色蒙版、底部的slogan图片、底部的地址信息这几个图片都可以同理嵌入到对应的位置，只需调整横纵坐标的参数即可。其中原图路径的`os.sep`是通配的路径分割符号，因为Windows和MacOS的路径分割符不一致，所以采用通配样式处理。

### 实时时间获取

利用Python的time库即可实时获取系统时间，文档如下。

```txt
%y 两位数的年份表示（00-99）
%Y 四位数的年份表示（000-9999）
%m 月份（01-12）
%d 月内中的一天（0-31）
%H 24小时制小时数（0-23）
%I 12小时制小时数（01-12） 
%M 分钟数（00=59）
%S 秒（00-59）
%a 本地简化星期名称
%A 本地完整星期名称
%b 本地简化的月份名称
%B 本地完整的月份名称
%c 本地相应的日期表示和时间表示
%j 年内的一天（001-366）
%p 本地A.M.或P.M.的等价符
%U 一年中的星期数（00-53）星期天为星期的开始
%w 星期（0-6），星期天为星期的开始
%W 一年中的星期数（00-53）星期一为星期的开始
%x 本地相应的日期表示
%X 本地相应的时间表示
%Z 当前时区的名
```

针对本项目的需求，只需要以下时间信息。

```python
# 将星期数字转换成为中文
def get_week_day(int):
  if int == 0 :
    return "周日"
  elif int == 1 :
    return "周一"
  elif int == 2 :
    return "周二"
  elif int == 3 :
    return "周三"
  elif int == 4 :
    return "周四"
  elif int == 5 :
    return "周五"
  elif int == 6 :
    return "周六"

# 获得相应的日期信息
nowNumberMonth = time.strftime('%m')  # 数字月份信息
# 因为获取的个位数数字月份带有0，所以将数字月份信息除了10月的0之外，其余月份的0全部删除
if int(nowNumberMonth) != 10 :
  nowNumberMonth = nowNumberMonth.replace('0','') 

nowEnglishMonth = time.strftime('%B')  # 获取英文的月份信息
nowEnglishMonth = nowEnglishMonth.upper()  # 全部转为大写

nowDay = time.strftime('%d')  # 获取数字日期信息

nowEnglishWeek = time.strftime('%A')  # 获取英文的星期信息
nowEnglishWeek = nowEnglishWeek.upper()  # 全部转为大写

nowChineseWeek = get_week_day(int(time.strftime('%w')))  #获取中文的星期信息
```

### 绘制时间信息

这一块是相对比较繁琐的一部分，先对整个时间模块的需求进行分析：

+ 日期信息的文字最大
+ 英文月份的左端和日期的左端对其
+ 数字月份的右端和日期的右端对齐
+ 英文+数字月份的长度等于日期的长度
+ 英文星期的长度等于日期的长度
+ 中文星期的位置要和日期的位置居中对齐
+ 英文星期的字体和其他信息的字体不同

先由第一行文字开始实现，首先要对全部的英文+数字月份组合字符串长度进行统计。

```txt
一月January---11个字符  
二月February---12个字符
三月March---9个字符
四月April---9个字符
五月May---7个字符
六月June---8个字符
七月July---8个字符
八月August---10个字符 
九月September---13个字符
十月October---11个字符
十一月November---14个字符
十二月December---14个字符
```

可以看出字符数量的波动范围很大，如果按照14这个最大长度进行适配，就会出现较在短字符月份时，英文月份和数字月份中间间距拉的过开的问题，一定程度上影响美观。于是决定以10个字符长度为分界线，做两套尺寸方案，即3~8月一个尺寸，其他月份另一个尺寸。根据上述思路，利用PS进行像素点定位，很容易就得到了两套尺寸方案的数据，3~8月使用较小尺寸，其他月份使用较大尺寸。

接下来是解决英文星期字母间距的问题。基本思路是根据当前月份的日期信息的长度，作为英文星期单词的总绘制长度。将这个长度除以当前英文星期单词的总字符数，即可得到每个字母之间的间距。然后将英文星期单词的每一个字母进行拆分，绘制完一个字母后，下一个字母绘制点的横坐标 = 上一个字母绘制点的横坐标 + 字符间距。利用for循环即可完成整个绘制过程。

最后是中文星期文字的绘制。由于都是4个字符的组合，借助PS测量绘制点即可，思路同绘制第一行。

整体代码如下：

```python
# 设置字体文件
timeFontDirOne = "." + os.sep + "Font" + os.sep + "timeFontOne.TTC"
timeFontDirTwo = "." + os.sep + "Font" + os.sep + "timeFontTwo.ttc"

# 设置各种文字字体大小，两套大小标准，需用if判断
if  2 < int(nowNumberMonth) < 9 : 
  timeFontSizeOne = 100
  timeFontSizeTwo = 620
  timeFontSizeThree = 70
  timeFontSizeFour = 100
else:
  timeFontSizeOne = 100
  timeFontSizeTwo = 860
  timeFontSizeThree = 70
  timeFontSizeFour = 100

# 设置每一行的字体总样式，字体和大小
timeFontCssOne = ImageFont.truetype(timeFontDirOne,timeFontSizeOne)
timeFontCssTwo = ImageFont.truetype(timeFontDirOne,timeFontSizeTwo)
timeFontCssThree = ImageFont.truetype(timeFontDirTwo,timeFontSizeThree)
timeFontCssFour = ImageFont.truetype(timeFontDirOne,timeFontSizeFour)

# 设置第一行时间文字起点坐标
if  2 < int(nowNumberMonth) < 9 : 
  timeFontLocationLeftX = 180
  timeFontLocationRightX = 650
  chineseWeekFontLocationX = 380
  timeFontLocationY = 3000
else:
  timeFontLocationLeftX = 180
  timeFontLocationRightX = 850
  chineseWeekFontLocationX = 500
  timeFontLocationY = 3000

# 设置画笔
draw = ImageDraw.Draw(bgImage)

# 第一行时间绘制--月份
draw.text([timeFontLocationLeftX, timeFontLocationY], nowEnglishMonth, "white", font=timeFontCssOne)
draw.text([timeFontLocationRightX, timeFontLocationY], nowNumberMonth + "月", "white", font=timeFontCssOne)

# 第二行时间绘制--日期
draw.text([timeFontLocationLeftX, timeFontLocationY + timeFontSizeOne], nowDay, "white", font=timeFontCssTwo)
#draw.text([timeFontLocationLeftX, timeFontLocationY + timeFontSizeOne], "02", "white", font=timeFontCssTwo)

# 第三行时间绘制--英文周几
nowEnglishWeekLen = len(nowEnglishWeek)  # 获取字符长度
if 2 < int(nowNumberMonth) < 9 : # 计算两套方案下的字母间距
  nowEnglishWeekWidth = (792 - timeFontLocationLeftX) / nowEnglishWeekLen
else :
  nowEnglishWeekWidth = (1065 - timeFontLocationLeftX) / nowEnglishWeekLen

tempTimeFontLocationLeftX = timeFontLocationLeftX
for i,s1 in enumerate(nowEnglishWeek):  # 挨个绘制字母
  draw.text([tempTimeFontLocationLeftX, timeFontLocationY + timeFontSizeOne + timeFontSizeTwo],s1, "white", font=timeFontCssThree)
  tempTimeFontLocationLeftX += nowEnglishWeekWidth  # 绘制完一个字母之后横坐标要加上间距

# 第四行时间绘制--中文周几 
draw.text([chineseWeekFontLocationX, timeFontLocationY + timeFontSizeOne + timeFontSizeTwo + timeFontSizeThree + 30], nowChineseWeek, "white", font=timeFontCssFour)

```

### 绘制语录

语录分为背景的黑色半透明蒙版和中文文字的绘制。添加图片和文字的方法基本和上文一致，确认绘制点和字体就好。这里主要要解决黑色半透明蒙版的长度要随文字长度自适应变化的问题，即文字输入多长，黑色蒙版就要有多长。

具体思路是，首先要求用户输入一串汉字，获取这段汉字的个数。然后在PS中计算一个汉字的长度，将文字个数乘以单个文字长度即可得到黑色蒙版的长度。在计算总长度是可以增加1~3个文字个数进行计算，文字后面留点空间会美观一些。

具体代码如下：

```python
statementFontSize = 130  # 设置字体大小
statementFontCss = ImageFont.truetype(statementFontDir,statementFontSize) # 设置字体总样式

# 获取语录
statement = input("输入今天的语录：")

# 语录坐标
maskLocationX = 170
maskLocationY = 0

# 绘制语录蒙版
maskScale = 1.2
statementLen = len(statement) # 获取字符长度
maskWidth = (statementLen + 2) * 120  # 计算蒙版长度
maskHeight = int(maskImage.size[1]*maskScale) # 设置蒙版长度
maskImage = maskImage.resize((maskWidth, maskHeight), Image.ANTIALIAS)  # 调整整体蒙版尺寸
r,g,b,a = maskImage.split()  # 色域分离，保证透明度
bgImage.paste(maskImage, (maskLocationX, maskLocationY + timeFontLocationY + timeFontSizeOne + timeFontSizeTwo + timeFontSizeThree + timeFontSizeFour + 120), mask=a)

# 绘制语录
draw.text([maskLocationX, maskLocationY + timeFontLocationY + timeFontSizeOne + timeFontSizeTwo + timeFontSizeThree + timeFontSizeFour + 130], statement, "white", font=statementFontCss)

```

## 0x04 总结

整体的代码就不贴了，强迫你们自己动手实践一下2333。如果不会用PS来测量像素位置的，其实用一些截图软件也可以，只是数据可能不是很精准，会误差个几十个像素，不过自己多调整几次参数也可以达到预期的效果。整体来说这个需求一点也不难，只是适配起来有点小繁琐，大家有类似需求的可以参考借鉴一下。
