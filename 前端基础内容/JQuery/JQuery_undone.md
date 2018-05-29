# jQuery #

----------

## jQuery引入方式: ##

`<script type="text/javascript" src="js/jquery-1.12.2.js"></script>`

## jquery的ready方法 ##
让文档加载完在执行
```JavaScript
// 第一种
$(document).ready(function(){
     ......
});

// 第二种
$(function(){
     ......
});

```

## jquery获取元素的方式 ##

**选取**元素

```
$('#myId') //选择id为myId的网页元素
$('.myClass') // 选择class为myClass的元素
$('li') //选择所有的li元素
$('#ul1 li span') //选择id为为ul1元素下的所有li下的span元素
$('input[name=first]') // 选择name属性等于first的input元素
```

对选取的元素**过滤**
```
$('div').has('p'); // 选择包含p元素的div元素
$('div').not('.myClass'); //选择class不等于myClass的div元素
$('div').eq(5); //选择第6个div元素
```

选择相关元素(父类/子类/前一个/后一个/其他),**选择集转移**
```
$('#box').prev(); //选择id是box的元素前面紧挨的同辈元素
$('#box').prevAll(); //选择id是box的元素之前所有的同辈元素
$('#box').next(); //选择id是box的元素后面紧挨的同辈元素
$('#box').nextAll(); //选择id是box的元素后面所有的同辈元素
$('#box').parent(); //选择id是box的元素的父元素
$('#box').children(); //选择id是box的元素的所有子元素
$('#box').siblings(); //选择id是box的元素的同级元素
$('#box').find('.myClass'); //选择id是box的元素内的class等于myClass的元素
```

## jquery操作样式属性 ##

形如:
`$("div").css({fontSize:"30px",color:"red"});`
可以连续操作
`$("div").css({fontSize:"30px",color:"red"}).siblings().css({fontSize:"500px",color:"blue"});`

操作样式类名
```
$("#div1").addClass("divClass2") //为id为div1的对象追加样式divClass2
$("#div1").removeClass("divClass")  //移除id为div1的对象的class名为divClass的样式
$("#div1").removeClass("divClass divClass2") //移除多个样式
$("#div1").toggleClass("anotherClass") //重复切换anotherClass样式
```

## jquery绑定事件 ##
常用事件:`click`点击,`animate`动画

```
$('#btn1').click(function(){

    // 内部的this指的是原生对象

    // 使用jquery对象用 $(this)

})
```
