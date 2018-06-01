# 关于QuerySets #

----------


1.filter和exclude返回对象都是QuerySets对象,类似list中间保存的是实例对象,可以迭代/循环/获取索引/切片(不支持负索引),切片出来的对象也是QuerySet.

2.QuerySets是**惰性**的操作,只有进行**evaluated**操作时才会真正的连接数据库进行查询操作,目的是 对查询进行优化 提高数据库查询效率，减少操作次数.(特例:当QuerySet切片操作带有`step`属性时会立刻执行)

3.对QuerySets的操作
```
.exists()  # 判断QuerySets是否有内容
.count()  # 判断QuerySets内容的数目(调用的是SELECT COUNT(*) from...)
.order_by(field)  # 对QuerySets进行排序(默认升序.`-field`降序,`?field`随机)
.distinct()  # 对QuerySets进行去重操作,多表查询可能会用到
.query  # 查询对应操作sql语句,需要print才能显示
.values_list()  # 元组[(),()...]方式对象的值,默认获取全部,填上字段名将获取相应的内容,flat=True正对一个字段,会让输出结果变成[a,b,...]
```