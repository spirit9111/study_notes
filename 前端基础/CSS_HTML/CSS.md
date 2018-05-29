# CSS #

CSS(Cascading Style Sheets)层叠样式表,简单来说就是用来修饰html的,将网页的基本骨架用html搭建,css来完成样式内容.

## 引入css的方式: ##

外链式:最常用的方式
`<link rel="stylesheet" type="text/css" href="css/main.css">`

内联式:直接写在html标签内,JavaScript设置的css都将是这种方式
`<div style="width:100px; height:100px; background:red ">......</div>`


嵌入式:将css与html混写,写在开头style内
```
<style type="text/css">
    div{ width:100px; height:100px; background:red }
    ......
</style>
```

## css选择器 ##

标签选择器(影响范围大,一般用于通用设置),

类选择器(灵活,可复用,最常用的方式),

层级选择器(用于嵌套结构之中)

## css样式属性(重要) ##

|属性名|介绍|
| --- | --- |
|  |  |
| **布局样式属性** |  |
|  |  |
| width | 宽度 |
| height | 高度 |
| background | 背景色 |
| border | 边框,包含top,bottom,right,left四个部分,可单独设置 |
| padding | 内边距,内容与边框的距离,包含top,bottom,right,left四个部分,可单独设置  |
| margin  | 外边距,块与块的边距,包含top,bottom,right,left四个部分,可单独设置  |
| float | 浮动,可以让块元素并列为一行,分为left,right两种 |
| display | 元素的类型和显示方式,none隐藏,inline以行内元素方式显示,block以块元素方式显示  |
| overflow | 溢出方式设置(子元素大于父元素),visible不作处理,hidden 裁剪溢出的内容,auto自动裁剪,内容以滚动方式展出 |
| border-collapse | 表格边线合并,collapse合并 |
| position | 定位设置(子绝父相),relative相对定位(相对自己,占位),absolute绝对定位(相对父级,不占位),fixed固定定位(相对浏览器),z-index层级设置   |
|  |  |
| **文本样式属性** |  |
|  |  |
| color | 字体颜色 |
| font-size | 字体大小 |
| font-family | 字体样式 |
| font-weight  | 字体加粗,bold加粗, normal不加粗|
| line-height | 行高,字体大小+边距,多行字体之间的宽度 |
| text-decoration | 下划线,none去除下划线,underline设置下划线,line-through中划线 |
| text-align | 文字对齐方式,center居中,left左对齐,right右对齐 |
| text-indent | 缩进 |
| list-style | 去除列表的原点 |


## 盒子模型 ##
![盒子模型](https://i.imgur.com/KZvSkZ3.jpg)
盒子的真是大小:

盒子宽度 = width + padding左右 + border左右

盒子高度 = height + padding上下 + border上下

## 块元素居中: ##
`margin:0px auto`

## 权重计算 ##

1、内联样式，如：style=””，权重值为1000
2、ID选择器，如：#content，权重值为100
3、类，伪类，如：.content、:hover 权重值为10
4、标签选择器，如：div、p 权重值为1