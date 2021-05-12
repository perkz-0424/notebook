### HTML超文本标记语言
~~~~
<meta charset="utf-8">
<html lang="en">告诉搜索引擎爬虫网站的内容,语言是英语
~~~~
##### SEO

##### 标签
~~~~
<p></p>
<div></div>
<span></span>
<strong></strong>加粗
<br>换行功能
<hr>水平分割线
<b></b>加粗
<em></em>斜体
<i></i>斜体 效果一摸一样
<small></small>小号字体
<sub></sub>下标
<sup></sup>上标类似于平方
<ins></ins>下划线 填写答案线
<del></del>中划线
~~~~
##### 实体字符
~~~~
空格 &nbsp;
小于号 &lt;
大于号&gt;
版权（圈c）&copy;
注册商标（圈R）&reg;
商标TM &trade;
~~~~
##### 有序列表  基本不用了
~~~~html
<ol> 
  <li></li>
  <li></li>
</ol>
~~~~
~~~~
ol里的属性type=“1/a/A/i/I/”1是数字排序，a是小写字母排序，A是大写字母排序，i和I罗马数字
ol里的属性reversed=“reversed”倒序
ol里的属性start=””从第几个开始排，里面写数字
~~~~

##### 无序列表
~~~~html
<ul> 
  <li></li>
  <li></li>
</ul>
~~~~
~~~~
只要type一个属性表示前面的标“disc”实心圆默认“square”方形“circle”是空闲圆
css里用list-style：none；来让前面没有任何标
~~~~
##### 自定义列表
~~~~html
<dl></dl>
<dt></dt>定义自定义列表的标题
<dd></dd>定义自定义列表的内容
    <dl>
        <dt>标题</dt>
        <dd>内容</dd>
    </dl>
~~~~
##### 图片标签
~~~~
<img src=””>单标签
属性src里有1.本地的url
       2.本地的绝对路径（地址写全）
       3.本地的相对路径（在同一个文件夹）
属性alt图片站位，当图片加载失败展示文字信息
属性title图片提示符
~~~~
~~~~html
<img src="logo2.png" alt="图片" title="这个是吸尘器">
~~~~
##### 超链接跳转
###### a标签的四个主要作用

###### 1.<a href=””></a>
~~~~
img标签被a标签包裹，img点击跳转
属性target 属性值为-blank时跳转时在新的页面
<a href="https://www.4399.com" target="blank"><img src="logo2.png" alt="跳转到小游戏" title="跳转到4399小游戏"></a>
~~~~
###### 2.a标签的锚点书签记录位置，通过a标签回到那，用id记录
~~~~
<div id=”ab”></div>
<a href=”#ab”></a>点击后回到上面的div
~~~~
###### 3.打电话发邮件
~~~~
<a href=”tel：138……”></a>打电话
<a href=”malito：138…@xx.com”></a>发邮件
~~~~
###### 4.里面放一个JavaScript代码 加书签功能

##### 表单标签  传数据必须有名有值
~~~~html
<form methon=”get/post” action=”后端地址”>
   <input type=”text”>文本框
   <input type=”password”>密码框
   <input type=”submit”value=”登录”>提交框
</form>
~~~~
~~~~
input的属性name数据名 有了数据名和数据值才能提交提交，框里有数据值
input的属性value 里面的文本内容
~~~~
##### 单选框
~~~~html
<input type=“radio”name=“x”value=“y”checked=“checked”id>
~~~~
~~~~
name属性就是让几个选项指向同一个问题，name的值要一样
要想提交数据必须加上value值，有名有值才能提交数据
某一个选项的属性checked的属性值设置成checked那这个选项就是默认选中
~~~~
##### 多选框
~~~~html
<input type=”checkbox”name=“x”value=”y”>
~~~~
##### 下拉菜单 也是写在form表单里
~~~~html
<select name=“x”>
   <option>1</option>
   <option>2</option>
   <option>3</option>
</select>
selected="selected"写在option里代表默认选项
~~~~
~~~~
不需要加value，里面是123就代表了值，名写在select上
~~~~
~~~~html
<textarea>xx</textarea>文本域一个很大的输入框
~~~~
~~~~
属性：rows行和cols列 调整大小
~~~~
~~~~html
<textarea name="" id="" cols="30" rows="10"></textarea>
<label for=“xx”></label>定义了<input id=“xx”></input>元素的标签，一般为标题，用属性for和id相连
~~~~
##### 外框，将文本标签包裹
~~~~html
<fieldest>
  <legend></legend> 外框标题
  <input type=”checkbox”name=“x”value=”y”>
</fieldest>
~~~~

##### 输入框的与选择消息提示
~~~~html
<input type="text" list="aa">
    <datalist id="aa">
        <option value="aaa">aaaa</option>
    </datalist>
~~~~
##### 按钮
~~~~html
<button></button>
~~~~
##### 表格标签
~~~~
第一步最外面用<table></table>包裹
第二步在<table></table>用<tr></tr>，做多少行的表格就写多好组<tr></tr>
第三步在<tr></tr>里插入列<th></th>表头单元格或者<td></td>普通单元格
~~~~
##### 表格属性 排版

~~~~
1.写在<table></table>上
border 外边框 不是内边框 
bgcolor背景颜色
cellpadding 内边距 内容到边的距离
cellspacing 外边距 内容整体与内容整体的距离
width设置成百分之百，自适应宽占满
<table border="1" bgcolor="#f40" cellpadding="10" cellspacing="20"></table>
~~~~

~~~~
2.写在<tr></tr>
align=“center”
height
~~~~

~~~~
3.写在<th></th>或者<td></td>
colspan 单元格可横跨的列数 一个格横向往后站几个格的位置
rowspan 单元格可纵跨的行数 一个格纵向往下站几个格的位置
bgcolor背景颜色
width
~~~~
##### 内联框架
~~~~
<iframe></ifarme>
可以嵌入其他其他网站，视频，可以实现页面内切换，不同a标签
属性
scrolling  yes/no是否可以滚动
~~~~

##### 音视频
~~~~
兼容性都不好
1.<embed>单标签
属性：height  width  src文件地址
~~~~
~~~~
2.<object></object>
属性：height  width  data文件地址
~~~~
~~~~
3.<audio></audio>只能播放音频
<audio controls>
  <source src=“xx.mp3”type=“mp3”>
</audio>
~~~~
~~~~
4.<video></video>只能播放视频
<video width=“320”height=“320”controls>
   <source src=“xx.mp4”type=“mp4”>
</video>
~~~~
###### 由于兼容性不好所以解决方法：
~~~~html
<video width=””height=””controls>
  <source src=””type=””>
  <object data=”” width=””height=””>
     <embed src=””width=””height=””>
</object>
</video> 

~~~~