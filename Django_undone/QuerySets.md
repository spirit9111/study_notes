# 关于QuerySet #

----------
QuerySet是**惰性**的操作,只有进行**evaluated**操作时才会真正的连接数据库进行查询操作,
目的是对查询进行优化,提高数据库查询效率,减少操作次数.

关于evaluated操作,常见的有以下几种:

- 迭代,也就是for循环
- 有step参数的切片操作
- Pickling/缓存
- repr()
- len(),查询QuerySets长度
- list(),强制转化QuerySet对象为list对象
- bool()

常见的返回全新QuerySet对象的API

| 方法名 | 介绍 |
| --- | --- |
| all() | 获取所有 |
| filter() | 对查询结果进行筛选 |
| exclude() | 反选,拍出满足条件的对象 |
| order_by(field) | 对QuerySets进行排序,(默认升序.`-field`降序,`?`随机) |
| reverse() | 反转排序 |
| distinct() | 去重,多表查询可能会用到 |
| values(*field) | QuerySet中以字典形式返回对象,形如[{x:'x'},{y:'y'},{z:'z'}] ,可以指定显示字段|
| values_list(*field) | QuerySet中以元组形式返回对象，形如[(x,'x'),(y,'y'),(z,'y')] |
| none() | 获取空的QuerySet |
| select_related() | 附带查询关联对象 |
| annotate() | 使用聚合函数 |










1.filter和exclude返回对象都是QuerySets对象,类似list中间保存的是实例对象,可以迭代/循环/获取索引/切片(不支持负索引),切片出来的对象也是QuerySet.

2.

3.对QuerySets的操作
```
.exists()  # 判断QuerySets是否有内容
.count()  # 判断QuerySets内容的数目(调用的是SELECT COUNT(*) from...)
.order_by(field)  # 对QuerySets进行排序(默认升序.`-field`降序,`?field`随机)
.distinct()  # 对QuerySets进行去重操作,多表查询可能会用到
.query  # 查询对应操作sql语句,需要print才能显示
.values_list()  # 元组[(),()...]方式对象的值,默认获取全部,填上字段名将获取相应的内容,flat=True正对一个字段,会让输出结果变成[a,b,...]
```