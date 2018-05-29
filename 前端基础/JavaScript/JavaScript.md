# JavaScript #

----------


## JavaScript嵌入方式 ##

外部引入,从.js文件引入,最为常用
`<script type="text/javascript" src="js/index.js"></script>`

行间引入,常用用于事件控制
`<input type="button" name="" onclick="alert('ok！');">`

页面script标签嵌入,html与js混用
```
<script type="text/javascript">        
    alert('ok！');
</script>
```


## 定义变量,变量类型,命名规则 ##

使用`var`关键字定义,
变量命名规则,字母/数字/`_`/`$`,区分大小写
一般首字母小写表示类型,


| 名称 | 类型 |
| --- | --- |
| number  | 数字类型 |
| string | 字符串 |
| boolean  | 布尔值 |
| undefined  | 用var声明但没有值 |
| null  | 空类型 |
| array | 数组类型,类似python列表 |

## 函数 ##

js函数执行顺序,先编译在执行(预编译),定义/执行不重要

```
//定义
function 函数名(形参){
        函数内容
    }

fnAlert();    //执行
```

封闭函数
```
// 第一种形式
!function(){
    alert('hello!');
}();

// 第二种形式
(function(){
    alert('hello!');
})();

// 第三种形式
~function(){
    alert('hello!');
}();
```

## if-else语句 ##

运算符基本规则不变,值的注意的是:
`==`只判断值是否相等(数字和数字形式的字符串可以相等)
`===`即判断类型也判断值是否相等
`&&`且
`||`或
`!`非

基本语法
```
var iNow = 1;
if(iNow==1)
{
    ... ;
}
else if(iNow==2)
{
    ... ;
}
else
{
    ... ;
}
```

## 获取元素,操作元素 ##

使用window.onload来保证js语句不会立即执行
```
window.onload=function(){
    
}
```
获取元素
`document.getElementById('id名')`等

操作元素

元素.属性名 = 新属性值 改写属性

注意`class`属性在js中应该写为`className`
所有带有`-`的属性需要去掉`-`并将后一个单词首字母大写.`font-size`，改成`style.fontSize`

`innerHTML `属性可以以字符串形式,获得包含标签在内的全部内容

## 常用事件 ##
`onclick`鼠标点击事件
`onmouseover`鼠标移入
`onmouseout`鼠标移出

## 数组定义,方法,属性 ##

| 方法/属性 | 介绍 |
| --- | --- |
| aList.length | 获取数组长度 |
| aList[0] | 获取索引为0的元素 |
| aList.join('任意字符') | 以字符拼接数组,以字符串形式输出 |
| **aList.push()** | 从末尾追加元素 |
| aList.pop() | 从末尾删除元素 |
| aList.reverse() | 反转数组 |
| **indexOf()** | 获取某元素第一次出现的索引 |
| **splice()**  | 增删元素,参数(索引,删除个数,追加的元素) |

## 字符串方法,属性 ##
| 方法/属性 | 介绍 |
| --- | --- |
| **+** | 合并,数字和字符串形的数字+操作将拼接 |
| parseInt() | 转化为整数 |
| parseFloat() | 转化为小数 |
| **split(任意字符)** | 将字符串以字符分离为数组 |
| indexOf() | 获取索引,多字符时返回首字符的索引 |
| **substring()** | 切片操作 |

## for循环 ##

类似python的while循环
```
for(var i=0;i<len;i++)
{
    ......
}
```

## 定时器 ##

`setTimeout`  只执行一次的定时器 

`clearTimeout` 关闭只执行一次的定时器

`setInterval`  反复执行的定时器

`clearInterval` 关闭反复执行的定时器