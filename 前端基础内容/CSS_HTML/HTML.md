# HTML #

HTML(HyperText Mark-up Language)是超(超链接)文本标(标签)记语言.


## 块元素标签 ##

默认占一行,

常用块元素:

`<h1></h1>`等标题标签,

`<p></p>`段落标签,

`<div></div>`通用块标签

`<table>`表格标签,内含`<tr>`行,`<th>`表头格,`<td>`普通单元格

`<form>`表单标签,一般内含`<input>`,`<label>`

`<ul>`列表标签,`action`属性表示提交的地址,`method`提交的方式(`get`,`post`)

## 内联元素标签 ##

默认在一行内并排,宽高属性无效,根据包含的内容自动调整.

常用内联元素:

`<a href="#">默认链接</a>`超链接标签,

`<span></span>`通用内联标签,

`<img src='' alt=''>`图片标签,其中img标签支持设置宽高

`<label>`表单的文字标注

`input`


## 常用的特殊标签 ##

`<br>`换行,

`<!-- 注释内容 -->`,

注释`&nbsp`空格,

`&lt`小于号,

`&gt`大于号

## input标签常用type属性 ##
`value`表单内的值
`name`提交数据的键名

| 属性 | 简介 |
| --- | --- |
| text | 文本输入框 |
| textarea | 多行文本输入框 |
| password | 密码输入框 |
| radio | 单选框 |
| checkbox | 多选框 |
| file | 上传文件 |
| submit | 提交按钮 |
| reset | 重置按钮 |
| button | 自定义按钮 |
| select | 下拉框 |
| option | 选项标签,与select搭配使用 |

display
块元素默认display:block;行内非替换元素(a,span)默认为display：inline;行内替换元素(input)默认为display:inline-block;
a.display:none;不显示该元素，也不会保留该元素原先占有的文档流位置。
b.display:block;转换为块级元素。
c.display:inline;转换为行内元素。
d.display:inline-block;转换为行内块级元素。

float
当把行内元素设置完float:left/right后，该行内元素的display属性会被赋予block值，且拥有浮动特性。行内元素去除了之间的莫名空白。

position
当为行内元素进行定位时，position:absolute与position:fixed.都会使得原先的行内元素变为块级元素。