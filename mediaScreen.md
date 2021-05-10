### 多媒体查询 响应式布局
~~~~css
随着屏幕尺寸的大小，布局发生变化
 @media screen and (min-width:992px) and (max-width:1200px){
    ul li{
        width: 30%;
        float: left;
    }
}
~~~~
~~~~html
根据大小可以写多个css文件然后引入到主css文件里
在head里引入，注意格式
<link rel="stylesheet" href="css.css" media=”screen and (min-width:992px) and (max-width:1200px)”>
~~~~
#### 一.检测的项目
~~~~html
1.viewport（视窗）宽度和高度
2.设备的宽度和高度
3.设备的朝向（横屏竖屏）
4.分辨率
<meta name="viewport" content="width=device-width,initial-scale=1,minmum-scale=1,maxmum-scale=1,user-scalable=yes">(这是适配手机端，只做pc端可以不写)
content的参数
width=device-width宽度等于手机宽度
initial-scale=1初始化尺寸为1倍
minmum-scale=1最小尺寸为1倍
maxmum-scale=1最大尺寸为1倍
user-scalable=yes可以手指滑动
~~~~
#### 二.多媒体查询语法
~~~~html
多媒体查询由多种媒体组成，可以包含一个或多个表达式，表达式根据条件是否成立返回true或false
@media not | only mediatype and (expressions) {css代码}
如果指定的多媒体类型匹配设备类型查询的结果返回true，文档会在匹配的设备上显示指定样式效果
除非你使用了not或者only操作符，否则所有样式会适应在所有设备上显示效果

not是用来排除某些特定的设备，比如@media not print（非打印机设备）

only用来定某种特别的媒体类型，对于支持Media Queries的移动设备来说，如果存在only关键字，移动设备的Web浏览器会忽略only关键词字并直接根据后面的表达式应用样式文件，对于不支持Media Queries的设备但能够读取Media Type类型的Web浏览器，遇到only关键字时会忽略这个文件样式
<link rel="stylesheet" media="mediatype and|not|only(expressions)" href="print.css">
all所有设备，这个应该经常看到
print用于打印机
screen用于电脑屏幕，平板，智能手机
speech用于屏幕阅读器
可以在不同媒体上使用不同的样式文件
~~~~
~~~~css
a常用于图片流
@media all and (max-width:1690px){...}
@media all and (max-width:1280px){...}
@media all and (max-width:980px){...}
@media all and (max-width:736px){...}
@media all and (max-width:480px){...}

b复杂的响应式
@media all and(min-width:1200px){...}
@media all and (min-width:960px)and(max-width:1199px){...}
@media all and (min-width:768px)and(max-width:956px){...}
@media all and (min-width:480px)and(max-width:767px){...}
@media all and(max-width:599px){...}
@media all and(max-width:479px){...}

基于Bootstrap3.x全球主流框架
@media all and(max-width:991px){...}
@media all and(max-width:768px){...}
@media all and(max-width:480px){...}

基于Bootstrap4.x全球主流框架
@media(min-width:576px){...}
@media(min-width:768px){...}
@media(min-width:992px){...}
@media(min-width:1200px){...}
~~~~
~~~~html
分多个写（css文件）然后分别引入
<link rel="stylesheet" media="screen and(max-width:768px)" href="print.css">
~~~~
~~~~
aspect-ratio定义输出设备中的页面可见区域宽度与高度的比率
color定义输出设备每一组彩色原件的个数。如果不是彩色设备，则值等于0
color-index定义在输出设备的彩色查询表中的条目数。如果没有使用彩色查询表，则值等于0
device-aspect-ratio定义输出设备的屏幕可见宽度与高度的比率。
device-height	定义输出设备的屏幕可见高度。
device-width	定义输出设备的屏幕可见宽度。
grid	用来查询输出设备是否使用栅格或点阵。
height定义输出设备中的页面可见区域高度。
max-aspect-ratio定义输出设备的屏幕可见宽度与高度的最大比率。
max-color定义输出设备每一组彩色原件的最大个数。
max-color-index定义在输出设备的彩色查询表中的最大条目数。
max-device-aspect-ratio定义输出设备的屏幕可见宽度与高度的最大比率。
max-device-height定义输出设备的屏幕可见的最大高度。
max-device-width	定义输出设备的屏幕最大可见宽度。
max-height定义输出设备中的页面最大可见区域高度。
max-monochrome定义在一个单色框架缓冲区中每像素包含的最大单色原件个数。
max-resolution定义设备的最大分辨率。
max-width定义输出设备中的页面最大可见区域宽度。
min-aspect-ratio定义输出设备中的页面可见区域宽度与高度的最小比率。
min-color定义输出设备每一组彩色原件的最小个数。
min-color-index定义在输出设备的彩色查询表中的最小条目数。
min-device-aspect-ratio定义输出设备的屏幕可见宽度与高度的最小比率。
min-device-width	定义输出设备的屏幕最小可见宽度。
min-device-height定义输出设备的屏幕的最小可见高度。
min-height定义输出设备中的页面最小可见区域高度。
min-monochrome	定义在一个单色框架缓冲区中每像素包含的最小单色原件个数
min-resolution定义设备的最小分辨率。
min-width定义输出设备中的页面最小可见区域宽度。
monochrome	定义在一个单色框架缓冲区中每像素包含的单色原件个数。如果不是单色设备，则值等于0
orientation定义输出设备中的页面可见区域高度是否大于或等于宽度。
resolution定义设备的分辨率。如：96dpi, 300dpi, 118dpcm
scan	定义电视类设备的扫描工序。
width定义输出设备中的页面可见区域宽度。
~~~~