###### 掌握


###### 超链接和锚点
```html
a标签:可定义锚(anchor),锚有两种用法：
    • 通过使用 href 属性，创建指向另外一个文档的链接（或超链接）;
    • 通过使用 name 或 id 属性，创建一个文档内部的书签（也就是说，可以创建指向文档片段的链接）;
<a href =”#A1”>第一章</a>  
<a href =”#A2”>第二章</a>
<a name =”A1”>第一章内容</name>
<a name =”A2”>第二章内容</name>
<a> 标签的两个重要属性:
href:它指链接的目标,也就是超链接关联的另一个资源;
taret:指定使用框架集中的哪个框架来装载另一个资源;属性值有:
    • _slef:表示自身,默认;
    • _blank:新窗口;
    • _top:顶层框架;
    • _parent:父框架;
<base>:标签为页面上的所有链接指定默认地址或默认目标;<base>必须位于 <head></head>标签之间;
<a>标签还可以发送邮件:
<a href="mailto:收件人邮箱?cc=抄送邮箱&subject=主题&body=内容">联系我</a>
```


###### 表格标签
```html
<table>:用于定义表格,<table>由0或1个<caption>子标签,0到1个<thead>子标签,0到1个<tfoot>子标签,多个<tr>子标签,多个<tbody>子标签组成;
<table>常用的属性如下:
	border:指定表格边框的宽度,默认是0;
	cellpadding:指定单元格内容和单元格边框的间距,值可是像素或百分比;
	cellspacing:指定单元格之间的间距,值可是像素或百分比;
	width:指定表格的宽度,值可是像素或百分比;
<caption>:用于定义表格的标题,必须放在<table></table>之间;
<tr>:定义表格行,该标签只能有<td>或<th>子标签;
<td>:定义单元格,放在<tr>中,表示把一行分成N个单元格;(N取决于N对<td>);	<td>常见属性如下:
    • colspan:指定该单元格跨多少列,属性值是数字;
    • rowspan:指定该单元格横跨的行数;
    • height:指定单元格的高度;
    • width:指定单元格的宽度;
<th>:定义表格页眉的单元格;用法和<td>标签一直,只是显示效果有差别;
<tbody>:定义表格的主体,该标签只能包含<tr>子元素;使用<tbody>标签可以将一个表格分成几个独立的部分;<tbody>可以讲表格里的一行或多行合并成一组,以后使用Ajax编程的时候常常需要动态修改表格的某几行,此时就得使用<tbody>标签了;
<thead>:定义表格头,用法和<tbody>一致,功能有点差别;
<tfoot>:定义表格脚,用法和<tbody>一致,功能有点差别;
<thead>,<tbody>,<tfoot>标签可以对表格的行进行分组,每对<tbody>就是一组;除此之外,当创建某个表格时.希望拥有一个标题行,以及底部的一个统计行;当打印表格式,表格头和表格脚的数据也会包含在数据的页面上;
无论<thead>,<tbody>,<tfoot>三者的先后顺序如何,页面上总会是最上面显示表格头,中间是显示表格体,最下面显示表格脚数据;一般开发中建议从上到下的顺序是:<thead>,<tfoot>,<tbody>;好处是即使网速慢没有加载出表格体的数据,但是表格头和表格脚的信息会先显示出来,以”安抚民心”;
```

```html
	<table border="1" width="100%" cellpadding="0" cellspacing="0">
		<caption>用户列表</caption>
		<thead>
			<tr style="background: gray;">
				<th>序号</th>
				<th>帐号</th>
				<th>状态</th>
			</tr>
		</thead>
		<tfoot>
			<tr align="center">
				<td colspan="3">
				<a href="#">首页</a>
				<a href="#">上页</a>
				<a href="#">下页</a>
				<a href="#">末页</a>
				</td>
			</tr>
		</tfoot>
		<tbody>
			<tr>
				<td>1</td>
				<td>11111</td>
				<td>在线</td>
			</tr>
			<tr>
				<td>2</td>
				<td>22222</td>
				<td>离线</td>
			</tr>
			<tr>
				<td>3</td>
				<td>33333</td>
				<td>隐身</td>
			</tr>
		</tbody>

```


###### 表单标签
```html
form标签,用于生成输入表单,该标签不可见;在HTML5之前,表单控件,如单行文本框,密码框,单选框等都必须放在<form></form>之间;常见属性如下:
    • action:必填属性,表示当点击”提交”按钮时,表单数据提交到哪个地址;
    • method:指定表单提交时的请求类型,该属性值有get或post,分别用于GET或POST请求,默认是get方式,开发建议使用post方式;
    • enctype:指定表单数据的编码方式,属性有3个值:

application/x-www-form-urlencoded
默认,只处理表单控件里的value属性值;
multipart/form-data
以二进制流的方式处理表单数据,文件上传时必须使用该属性值;
text/plain
不对特殊字符编码,适合于表单的属性值为mailto”URL形式,也就是说该方式适用于表单邮件的发送;
```

```html
<body>
	<h3>用户注册</h3>
	<form action="#" method="get">
		帐号：<input type="text" name="username" value="默认值"/><br/>
		密码：<input type="password" name="pwd" /><br/>
		性别：
			<input type="radio" name="gender" checked/>男
			<input type="radio" name="gender"/>女
			<input type="radio" name="gender"/>保密<br/>
		爱好：
			<input type="checkbox" name="hobby" checked/>Java
			<input type="checkbox" name="c"/>c
			<input type="checkbox" name="obj-c"/>obj-c<br/>
		头像：
			<input type="file" name="headImg"/><br/>
		城市：
			<select name="city" multiple size="4">
				<option value="gz">广州</option>
				<option>佛山</option>
				<option>潮汕</option>
				<option>深圳</option>
			</select><br/>
		简介：
			<textarea name="intro" rows="5" cols="30">aaa</textarea><br/>
		<input type="image" value="images/nextpage.png"/>
		<input type="button" value="普通按钮"/>
		<input type="submit" value="注册"/>
		<input type="reset" value=”重置“ />
	</form>
</body>
```

```html
  html5 表单新特性
<body>
<h3>用户注册</h3>
	<form action="#" method="get">
		帐号：<input type="text" name="username" required/><br/>
		邮箱：<input type="email" name="eml" /><br/>
		生日：<input type="date" name="age" /><br/>
		手机：<input type="email" name="eml" /><br/>
		<input type="number" name="keyword" max="10" min="1" placeholder="1-10"/>
		<input type="reset" value=”重置“ />
	</form>
</body>

```

###### input标签
```html
input标签,表单控件标签里功能最丰富的,用于接收用户输入的信息.
其中的type属性指定输入标签的类型。
    • 单行文本框:type = text,输入的文本信息直接显示在框中;
    • 密码输入框:type = password,输入的文本以圆点形式显示;
    • 单选框:type = radio,如：性别选择;
    • 复选框:type = checkbox,如：多个兴趣选择;
    • 隐藏域:type = hidden, 在页面上不可见,但在提交的时候会一起提交数据,用于隐式向后台传输一个数据;
    • 提交按钮:type = submit,用于提交表单中的数据内容;
    • 重置按钮:type = reset,将表单中填写的内容均设置为初始值;
    • 无动作按钮:type = button,可使用javascript为其自定义事件;
    • 文件上传域:type = file,会生成一个文本框和一个浏览按钮;
    • 图像域:type = image, 它可以替代submit按钮,即图像提交按钮。
<input>标签其他通用属性:
    • name:指定input标签的名字,没有设置name属性的标签不能提交数据;
    • value:指定input标签的初始值;
    • checked:设置单选框,复选框的初始状态是否选中;
    • disable:设置input标签加载时禁用此标签;
    • maxlength:文本框输入最大字符数,属性值是数字;
    • readonly:指定文本框内值不允许直接修改;
```




  

###### 框架标签
![[框架标签.png]]

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>

<frameset rows="5%,*,5%">
	<frame src="top.html"/>
	<frameset cols="200,*">
	
	<frame src="menu.html" noresize>
	<frame src="welcome.html" name="main"/>

	</frameset>
	<frame src="foot.html"/>
</frameset>
<noframes>
<body>
浏览器版本太低
</body>
</noframes>
</html>

```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
haha
haha
<iframe src="register.html">
</iframe>
haha
haha
</body>
</html>
```