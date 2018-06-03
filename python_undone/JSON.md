# JOSN基本内容 #

----------

## 关于JSON ##

json是 JavaScript Object Notation 的首字母缩写,意思是javascript对象表示法,类似javascript的对象,但是并不一样.

JSON用于在不同的编程语言之间传递对象(对象序列化), JSON 表示
出来就是一个字符串，可以被所有语言读取，也可以方便地存储到磁盘或者通过网络传输。

json和JavaScript区别:

1.json中没有函数,只有**属性**
2.json中的键值对必须使用`" "`**双引号**
3.支持复杂的数据结构,多层嵌套.

```
{
    "name":"jack",
    "age":29,
    "hobby":["reading","travel","photography"]
    "school":{
        "name":"Merrimack College",
        "location":'North Andover, MA'
    }
}
```