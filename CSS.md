### CSS cascading style sheet 重叠样式表
#### 一.引入css
##### 1.行间样式
~~~~html
<div style=“width:100px;”></div>
~~~~

##### 2.页面级css
###### 在head标签里写一个style标签
~~~~html
<style type=“text/css”>
     div{
       width:100px;
}
</style>
~~~~

##### 3.外部引入css文件
~~~~html
<link rel="stylesheet" href="lesson4.css">
~~~~
###### 然后在css文件里写
~~~~css
div{
    width:100px;
}
~~~~
~~~~
在css文件里导入另一个css文件
@import'另一个css文件名.css';
前提是两个css文件要在同一个文件夹下
~~~~

#### 二.选择器
##### 1.id选择器 
~~~~
用#id{}  一对一的
~~~~

##### 2.class选择器 
~~~~
用.class{ }  class选择器不是一一对应的 class选择器的值之间可以用空格隔开，表示多个<div class=“demo demo1”></div>
~~~~

##### 3.标签选择器
~~~~
直接写标签名就好
~~~~

##### 4.通配符选择器* 
~~~~
选择所有
~~~~

##### 5.属性选择器
~~~~
[class=“only”][id]用标签上的属性用中括号包起来作为属性选择器，名一定要写，值不一定写。
~~~~

##### 6.父子选择器
~~~~
div span.box{ } 一层套一层，中间是空格，不一定要都是一样的选择器 
~~~~

##### 7.直接子元素选择器
~~~~
div> span{ }只能选择连着的下一级，不能跳级，中间用>
~~~~

##### 8.并列选择器
~~~~
<div class=“demo”></div>
div.demo{} 不加空格中间 同一层用两个同时描述一个
~~~~

##### 9.分组选择器
~~~~html
<em></em>
<strong></strong>
<span></span>
~~~~
~~~~
em, 
strong, 
span{ }
让不同的标签拥有同一css样式。
~~~~

#### 三.优先级
~~~~css
div{
  width:100px!important;
}
~~~~
~~~~
!important>行间样式>id>class/属性>标签选择器>通配符
~~~~
~~~~
css权重
important        Infinity
行间样式           1000
id               100
class/属性/伪类    10
标签选择器/伪元素    1
通配符             0
进制256进制
权重相加判断值大小
~~~~

#### 四.CSS代码

##### 1.字体设置
~~~~
font-size:16px;默认的，字体大小设置是设置字体的宽
font-weight:bold;加粗
font-style:italic斜体
font-family:arial乔布斯字体
color就是设置字体颜色
opacity：0.5；透明度百分之50%
~~~~
##### 2.颜色设置的三种方法 transparent透明色
~~~~
1.red
2.#ff4400
3.rgb(255,255,255)
~~~~
~~~~
border:盒子的外边框 粗细 样式 颜色
~~~~

##### 3.画三角形
~~~~
用border来画三角形
border：100px solid black；
width：0px；
height：0px；
border-left-color：transparent；
border-right-color：transparent；
border-top-color：transparent；
单设置border它由内容去撑开
~~~~

#### 五.文本
~~~~
text-align：center居中表示 left左对齐
line-height:30px单行文本所占高度 垂直居中
(凡是带inline的元素都有文本元素的特点)
text-indent：2em；首行缩进两个字符，相对单位em
1em=1 font-size默认font-size16px
text-decoration:line-throngh;的样式等于<del><del>表示中划线
underline 下划线
text-decoration:none;文本样式消失
vertical-align调一行文字的对齐线
~~~~
~~~~
cursor：…当鼠标移入的光标变化
~~~~
#### 六.伪类选择器
~~~~
a：hover{ }鼠标移入
a：link{ }未访问
a：visited{ }已访问
a：active{ }点击
a：focus{ }聚焦
~~~~
#### 七.display

##### 1.行级元素：
~~~~
（inline）1>内容决定元素所占位置大小
         2>不可以通过css改变宽高
         如：span strong em a del b
~~~~

##### 2.块级元素：
~~~~
（block）1>独占一行
        2>可以通过css改变宽高
       如：div p ul li ol form address
~~~~
##### 3.行级块元素：
~~~~
（inline-block）1>内容决定大小
               2>可以改变宽高
               如：img
~~~~
~~~~
display是可以改，所以上述的display的值可以改，改完就变了
  1.凡是带有inline属性的都带有文字属性，就会被分割，多个连着img就会被分割
  2.一旦一个行级块元素里有文字了，外面的文字就会和里面的文字底对齐
~~~~
~~~~
值为none的时候就是隐藏元素,空间也会不见，是彻底隐藏
visibility:hidden;这个隐藏式表示空间还在的隐藏，只是隐藏了内容
当visibility:visible;时内容可见，可以做二级菜单
~~~~
#### 八.标签初始化自定义
~~~~
text-decoration:none;
padding:0;
margin:0;
list-style:none
~~~~

##### 样式初始化
~~~~css
*{
margin:0;
padding:0;
} 
body{
font:12px"宋体","Arial Narrow",HELVETICA;background:#fff;
-webkit-text-size-adjust:100%;
} 
a{
color:#2d374b;
text-decoration:none;
} 
a:hover{
color:#cd0200;
text-decoration:underline;
} 
em{
font-style:normal;
} 
li{
list-style:none;
} 
img{
border:0;
vertical-align:middle;
} 
table{
border-collapse:collapse;
border-spacing:0;
} 
p{
word-wrap:break-word;
}
~~~~
#### 九.盒子模型

##### （1）盒子的三大部分
~~~~
0.外边线：outline 只能设置四边且是个矩形 输入框有自带的设置成none就消失了
1.盒子壁：border
2.内边距：padding
3.盒子的内容：width+height
4.外边距:margin
~~~~
##### （2）padding(两个盒子嵌套，宽高一样，用外边盒子设置padding就可以成为一个中心嵌套)
~~~~
padding margin设置
四个值的时候是上  右  下  左
三个值的时候是上  左右  下
两个值的时候是上下   左右
~~~~
##### （3）
~~~~
body有一个天生的margin有8px
~~~~
##### （4）
~~~~
margin：0 auto 容器就居中了 自适应
border-radius圆角，四个值的话，左上 右上 右下 左下
~~~~

#### 十.css3盒子阴影
~~~~
box-shadow：120px 20px 20px -10px blue inset，120px 20px 20px -10px blue;
有六个值分别是：
1.h-shadow 必写，水平阴影位置，可写负值
2.v-shadow 必写，垂直阴影位置，可写负值
3.blur 选写，模糊距离
4.spread 选写，阴影大小
5.color 选写 阴影颜色
6.inset 不写默认是外层阴影，写上变成内阴影
用逗号隔开表示多重阴影
~~~~

#### 十一.层模型
~~~~
定位
position 
absolute：绝对定位，脱离原来位置进行定位，去了上一个层，让出原来层的位置，相对于最近的有定位的父级进行定位（可以是父级的父级），如果父级没有定位，那就相对于文档进行定位
relative：相对定位 保留原来位置进行定位，去了上一个层，但原来的层位置不让出，相对于原来的位置进行定位
fixed：固定定位在一个地方，
static：默认静态定位
position设置完后 系统会内部设置成inline-block
用left，right，top，bottom去设置位置

相对于文档的居中用
用position:absolute;
left:50%;
top:50%;
margin-left:-width/2;
margin-top:-height/2;
！！z-index
只在position使用表示层级在第几层
与position配合使用
~~~~
#### 十二.Bug
#####（1）margin塌陷
~~~~
现象：垂直方向（top）的margin父子元素是结合在一起的，父子margin合并，子元素的margin大于父级的margin时会带着父级一起动。
原因：父级元素和子级元素的顶部边紧贴
解决方法
1.父级加一个border-top
2.bfc 块级格式化上下文 block format context
3.不用margin用padding
~~~~
~~~~
如何触发bfc
1.position:absolute;（以及flex）
2.display:inline-block;（以及table-cell，table-caption，flex，inline-flex）
3.float:left/right;（float不等于none）
4.overflow:hidden;（overflow不等于visible）
凡是设置了position:abolute; float:left/right系统会从内部把元素设置成inline-block
~~~~

#####（2）margin合并
~~~~
现象：兄弟元素垂直方向上margin-top和margin-bottom合并了，导致兄弟元素在下面的元素的margin不好使了，但这个不用解决
~~~~

#### 十三.浮动模型
~~~~
float：left/right；左浮动/右浮动（加了之后产生了bfc）
能使元素站队
！浮动元素产生了浮动流（站队），所有产生了浮动流的元素，块级元素看不到他们（看不到站队现象）。产生了bfc的元素和文本类元素以及文本都能看到浮动流元素（可以站队）。
~~~~
#### 十四.去除浮动流
~~~~
在最后一个浮动流元素的后面加一个p标签里面加一个
clear：both；
~~~~

#### 十五.伪元素 
~~~~
天然存在，可以当元素操作，但没有html结构，是行级元素
标签：：before{ }
标签：：after{ }
里面必须有content：“”；
~~~~

#### 十四-2去除浮动流
~~~~
父级标签::after{
  content:“”;
  display:block;（能清除浮动的必须是块级元素，伪元素是行级元素，所以必须改成块级元素）
  clear:both;
}
~~~~
#### 十六.溢出容器的，打点展示
##### 1.单行文字
~~~~
到边不换行
white-space:nowrap;
overflow:hidden;溢出隐藏
text-overflow:ellipsis;打点
~~~~
##### 2.多行文本
~~~~
手动打点
~~~~

#### 十七.背景图片
##### 1.设置图片
~~~~
background-image:url(fy.jpg);
~~~~

##### 2.设置背景图片的大小
~~~~
background-size:宽，高;
铺不满容器就会重复平铺图片
background-size:no-repeeat;
图片不重复铺，只出现一张
~~~~
##### 3.图片在容器中的位置
~~~~
background-position：100px 100px;
~~~~

##### 4.补充：
~~~~
1.padding上也可以有图片
2.行级元素只能嵌套行级元素
3.块级元素可以嵌套任何元素
4.a标签里不能套a标签
~~~~

#### 十九.引入iconfont
##### css文件里：
~~~~css
@font-face {
    font-family: 'iconfont';
    src: url('../font_6t8mrcwrvzt/iconfont.eot');
    src: url('../font_6t8mrcwrvzt/iconfont.eot?#iefix') format('embedded-opentype'),
        url('../font_6t8mrcwrvzt/iconfont.woff2') format('woff2'),
        url('../font_6t8mrcwrvzt/iconfont.woff') format('woff'),
        url('../font_6t8mrcwrvzt/iconfont.ttf') format('truetype'),
        url('../font_6t8mrcwrvzt/iconfont.svg#iconfont') format('svg');
  }
  .iconfont {
    font-family: "iconfont" !important;
    font-size: 16px;
    font-style: normal;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }
~~~~
##### html文件里：
~~~~html
<span class="iconfont">&#xe610;</span>
~~~~
#### 二十.css的列表属性（ul、ol）
~~~~
list-style主要是针对ul ol
三个值
1.list-style-image 图片
2.list-style-position 位置
3.list-style-type 样式
~~~~
##### 二十一.淘宝项目

#####1.样式重置模块化
~~~~
vertical-align: middle;图片垂直方向上与文字的对齐
font: 12px/1.5 tahoma,arial,'Hiragino Sans GB','\5b8b\4f53',sans-serif;
分别是：字体大小/行高 font-family
outline: none;
font-family:‘宋体’；这样写也可以
~~~~
##### 2.line-height不同值的区别
~~~~
行高可以给上五种值：normal 由浏览器和字体决定 字体不同默认行高不同
1.5 默认px乘1.5 （子元素继承1.5，其他种类的值都是继承计算过得px）
200%  默认px乘200% 
50px 固定值
5em 默认px乘5
~~~~
##### 3.预定样式
~~~~
包括清除浮动，左浮动，右浮动，自适应居中，左右边距等等
~~~~
##### 4.css@规则
~~~~
@charset ‘utf-8’ 设置样式表的编码
@import 导入其他css样式文件
@meida 移动端媒体查询
@font-face 自定义字体，自定义图标
~~~~
##### 5.favicon
~~~~
淘宝网-淘！我喜欢前面的小图标如何生成
1-先将图片生成ico文件放在根目录中
2-在html文件的head标签里引入
<link rel="icon" href="xxxx.ico">
~~~~

##### 6.base标签(在head标签里只能出现一个base标签)
~~~~
<bade href=”” target=”_blank”>
统一用于a标签跳转的地址设置设置了target=”_blank”,那么所有页面所有的a标签跳转都在新页面里
~~~~
##### 7.自定义图标
~~~~
阿里巴巴的iconfont的使用
1-搜索图标
2-添加入库
3-下载代码
4-打开下载包里的demo_index.html文件
5-按照文件里的步骤（使用Unicode的栏目）
 第一步：拷贝第一段代码项目下面生成的 @font-face，放在css文件中
 第二步：把下载的包里的iconfont.eot iconfont.svg iconfont.ttf iconfont.woff iconfont.woff2这五个文件 复制到根目录的font文件夹里
 第三步：修改复制过来的五个文件的地址
 第四步：定义使用 iconfont 的样式，复制代码第二段代码到css文件
 第五步：挑选相应图标并获取字体编码，应用于页面
按这个格式引用到html文件里<span class="iconfont">&#x33;</span>
6-在demo_index.html打开的界面里找到图标代码复制过来
可以修改第二段代码里的font-size设置整体大小
~~~~

##### 8.H标签的应用场景
~~~~
h1-h6爬虫权重依次递减，板块标题用h3
~~~~
##### 9.以图换字
~~~~
1-在css标签里用background:url(../images/logo.png);导入图片
2-css文件里写text-indent: -9999px;
3- overflow: hidden;
~~~~
##### 10.怪异盒子模型
~~~~
padding的添加会把原先的盒模型撑大，
box-sizing:border-box;变成了怪异盒模型
盒模型的种类：
  1-标准的盒模型 总宽度=border（左右）+width+padding（左右）高度一样
  2-怪异的盒模型 总宽度=width （添加padding和border会基于固定的width让真实的width会计算以后会改变）高度一样
~~~~
##### 11.css3圆角和颜色渐变过度
~~~~
  border-radius: 左上 右上 右下 左下;  
  线性渐变background-image: linear-gradient(方向头right，起始的颜色，结束的颜色 );ie10以上
  方向：可以写135deg表示角度表示从左上角到右上角
~~~~

##### 12.IE滤镜
~~~~
  也是渐变ie10以下,功能强大
  filter: progid:DXImageTransform.Microsoft.gradient(startColorstr='#ffff9000', endColorstr='#ffff5000', GradientType=1);
~~~~
##### 13.CSS HACK 设置css的浏览器的版本使用
~~~~
  background-color:#000\9; IE9以下浏览器可以使用，也就是IE8可以用
~~~~
##### 14.图片垂直居中对齐
~~~~
1-带有inline属性（img带有）的都可以通过text-align：center；去居中对齐
2-display:table-cell;
  vertical-align:middle;
3-css3弹性盒模型居中对齐
   display:flex;
   justify-content:space-around;
   align-items:center;
~~~~

##### 15.CSS3 Sprites雪碧图 
~~~~
把小图标放在一个图片上，在利用定位分别使用，优化减少带宽
 background: #ffe4dc url(../images/ico.png) 0 -572px no-repeat;
0是x轴，-572是y轴，移动定点到小图标位置
也可以单独设置background-position: 0 -308px;
~~~~

##### 16.表格
~~~~
 优势：有边框，能居中，能自动计算宽度
 1-有边框：内部的边框不会重叠
td{
    border: 1px solid #f4f4f4;
}
 2-能居中能自动计算宽度：
 table {
    width: 100%;
    height: 231px;
    background-color: #fff;
    table-layout: fixed;
    /*定义列宽的算法 fixed的计算方式根据表格宽度自动计算列宽，每列的宽度均分整个表格的宽度*/
}
 border-spacing:0px;去中间的缝隙
~~~~
##### 17.图片格式webp
~~~~
   体积小 清晰度不变 兼容性不好
~~~~

##### 18.词换行
~~~~
   先在html中用空格隔开，然后在css中写入word-break: keep-all;表示以空格换行
~~~~

#####19.其他
~~~~
1-span是行级元素两个span元素在一起换行会产生空格，空格的大小由font-size决定，
所以通过父级分font-size设为0，自己重新设置font-size来消除空格

2-a标签是行级元素，所以点击的区域较小，改成display：block让他变成块级元素，横向的点击范围会变大

3-带有inline属性（img带有）的都可以通过text-align：center；去居中对齐

4-鼠标移入变成手：cursor: pointer;

5-用position: absolute;
    z-index: 2;
background-color: transparent;
解决搜索框的文字把搜索框覆盖了的问题

6-计算剩余宽度的方法width: calc(100% - 190px); ie9以上，注意减号前后的要有空格

7-css3过度背景色，在hover事件里颜色过度自然，在原来hover前的css（不是在hover里加）样式里添加transition: background-color 0.3s（在0.3里把颜色过度）这样就会有一个柔和的过度

8-css3rgba(红，绿，蓝，透明);ie9以上
ie9以下：
background-color：000\9;
filter:alpha( opacity=30);
     
 9 -moz代表firefox浏览器私有属性
-ms代表IE浏览器私有属性；
-webkit代表chrome、safari私有属性；
-o代表Opera私有属性。
~~~~
### css3

####二十二.过渡
~~~~
transition(属性值的变化)
过渡是从一个状态到另一个状态配合：hover、：active等使用
一共有四个属性依次是
1-property过渡的属性名
2-duration 过渡花费的时间
3-time-function 过渡方式线性还是别的
4-delay 过渡从多少时间后开始
~~~~
~~~~css
div{
    width: 20px;
    height: 20px;
    background-color: red;
    border-radius: 0;
}
div:hover{
    border-radius:50%;
    transition: border-radius 1s linear 100ms;
}
~~~~
#### 二十三.2D变换效果（位置 旋转 尺寸 倾斜变换）
~~~~
transform(多个值之间用空格)

1-位置变化
translate（*px/%）两个值x轴和y轴（逗号隔开）

2-旋转
rolate（*deg）

3-尺寸变化
scale（x,y）里面写的值是倍数

4-倾斜
skew(*deg，*deg)
~~~~
#### 二十四.3D变化（相对于2d是多了一个z轴上的变化属性值和2d一样）
~~~~
增加一个加在父级上的属性transform-style，属性值为preserve-3d时为3d效果
还有一个近大远小的效果，也是加在父级，perspective表示景深多上像素，值是**px
~~~~
#### 二十五.css3动画
~~~~
1-@keyframes创建动画
@keyframes name {
    0% {}
    33% {}
    66% {}
    100% {}
}
2-属性是animation（那个css样式需要就写在哪）
1>属性值有1/animation-name动画名
              2/animation-duration 动画的周期时间默认是0
              3/animation-timing-function动画的速度曲线默认是ease
              4/animation-delay动画从多少时间后开始默认是0
              5/animation-iteration-count动画播放的次数，默认是1 值为Infinite为无限次
              6/animation-direction动画下一个周期是否逆向播放，默认是normal
2>规定动画是否运行或暂定，用animation-play-state默认第running运动/paused是暂停
3-属性是animation-fill-mode
  1>属性值有1/none默认值不会有任何其他样式返回初始
             2/forwards动画结束停留在最后
             3/backwards
             4/both
~~~~
#### 二十六.渐变
~~~~
分为线性渐变和径向渐变
1-线性渐变
  background:linear-gradient(起始位置，颜色1 百分比，颜色2 百分比，颜色3…);
2-径向渐变
  background:radial-gradient(起始圆心点，形状，颜色1百分比，颜色2百分比…);
~~~~
#### 二十七.多媒体查询 响应式布局
~~~~
  随着屏幕尺寸的大小，布局发生变化
 @media screen and (min-width:992px) and (max-width:1200px){
    ul li{
        width: 30%;
        float: left;
    }
}
根据大小可以写多个css文件然后引入到主css文件里
在head里引入，注意格式
<link rel="stylesheet" href="css.css" media=”screen and (min-width:992px) and (max-width:1200px)”>
~~~~
#### 二十八.弹性盒子
~~~~
 必须给父级display:flex
~~~~
##### 1属性flex
~~~~
 加在子级 加flex：1表示所有子元素1比1的均分
 属性值：1.flex-basis基准宽度
         2.flex-grow：1；扩展量填写1就可以
         3.flex-shrink：1；收缩量填写1就可以
~~~~
##### 2父级加的属性justify-content单行的排版（子元素不加flex）
~~~~
属性值：1.flex-start排版在页面左边
        2.flex-end排版在页面右边
        3.center排版在页面中间
        4.space-arround全对齐
        5.space-between两边对齐两边不留空
~~~~

##### 3父级加的属性align-items单列的排版，父级有高度（子元素不加flex）
~~~~
属性值：1.stretch拉伸适应容器，默认
        2.center容器中心
        3.flex-start容器开头
        4.flex-end容器结尾
        5.baseline项目位于容器的基线上
~~~~
##### 4父级加的属性align-content多行的排版（子元素不加flex）
~~~~
属性值：1.stretch拉伸适应容器，默认
        2.center容器中心
        3.flex-start容器开头
        4.flex-end容器结尾
        5.space-arround上下左右均分空白
        6.space-between每行两边对齐，上下面不留空白，也就是四边不留空
~~~~
##### 5父级加的属性flex-wrap空白处理，换行换列（也需要自己的width的配合）
~~~~
属性值：1.nowrap 不拆行不拆列
        2. wrap 拆行拆列
        3.wrap-reverse 拆行拆列且反转
~~~~
##### 6子级加的属性align-self单个子元素垂直排版
~~~~
属性值：1.auto基础父级的align-items如果没有为stretch拉伸适应容器
        2.stretch拉伸适应容器
        3.center容器的中心
        4.flex-start容器开头
        5.flex-end容器结尾
        6.baseline项目位于容器的基线上
~~~~
##### 7父级加的属性flex-direction控制方向
~~~~
属性值：1.row不变，默认
        2.row-reverse每个子元素的位置水平翻转
        3.column行变列，列变行
        4.column-reverse行变列，列变行，然后子元素再水平翻转
~~~~
#####8子级加的属性order控制子元素的排序
~~~~
属性值：是数字，数字越大排在越前面可以负数
~~~~

