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
取出当前对象
```
$('#btn1').click(function(){

    // 内部的this指的是原生对象

    // 使用jquery对象用 $(this)

})
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
常用事件:
```
click()点击
blur() 元素失去焦点
focus() 元素获得焦点,一般不绑定函数,而是直接使用.focus()让输入框默认获得焦点.
click() 鼠标单击
mouseover() 鼠标进入（进入子元素也触发）
mouseout() 鼠标离开（离开子元素也触发）
mouseenter() 鼠标进入（进入子元素不触发）
mouseleave() 鼠标离开（离开子元素不触发）
hover() 同时为mouseenter和mouseleave事件指定处理函数
ready() DOM加载完成
submit() 用户递交表单
```


## jquery动画相关 ##

fadeIn() 淡入
fadeOut() 淡出
**fadeToggle() 切换淡入淡出**
hide() 隐藏元素
show() 显示元素
**toggle() 切换元素的可见状态**
slideDown() 向下展开
slideUp() 向上卷起
**slideToggle() 依次展开或卷起某个元素**

## jquery属性操作 ##

html()可以取出/设置对应标签内的代码块
```
// 取出html内容
var $htm = $('#div1').html();

// 设置html内容
$('#div1').html('<span>添加文字</span>');
```

prop()取出/设置某个属性
```
// 取出图片的地址
var $src = $('#img1').prop('src');

// 设置图片的地址和alt属性
$('#img1').prop({src: "test.jpg", alt: "Test Image" });
```

## 事件冒泡: ##

简单来说就是,子级对象的事件将从内到外传递,所有的父级对象同一类型的事件都将被触发,直到传递到最顶层的document对象.

特点:
从内到外
同一类型的事件才会被触发
不论什么样的事件其实都会被被传递(即使没有相应的事件,如果有则触发并继续向上传递,如果没有则本级略过,但是依旧向上传递.)

**阻止事件冒泡**的方法:
```
event.stopPropagation(); // 阻止冒泡
event.preventDefault();  // 阻止默认行为 

// 合并写法：
return false;

```

事件冒泡的应用:**事件委托**

事件委托就是把事件加到父级上，通过判断事件来源的子集，执行相应的操作，事件委托首先可以极大**减少事件绑定次数**，**提高性能**；其次可以让新**加入的子元素也可以拥有相同的操作**。

事件委托的形式:
`.delegate(子级,事件,回调函数)`

```
$(function(){
    $list = $('#list');
    $list.delegate('li', 'click', function() {
        $(this).css({background:'red'});
    });
})
...
<ul id="list">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
</ul>
```

## Dom操作 ##
dom操作(元素节点操作)指的就是改变html结构的操作.

创建新标签
```
var $div = $('<div>');  //创建一个空的div

var $div2 = $('<div>这是一个div元素</div>');
```

对html结构的操作:

1、append()和appendTo()：在现存元素的内部，从后面放入元素

2、prepend()和prependTo()：在现存元素的内部，从前面放入元素

3、after()和insertAfter()：在现存元素的外部，从后面放入元素

4、before()和insertBefore()：在现存元素的外部，从前面放入元素




