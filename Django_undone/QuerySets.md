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

## 常见操作QuerySets方法 ##

| 方法名 | 介绍 |
| --- | --- |
| **返回全新QuerySet** |  |
| all() | 获取所有 |
| filter() | 对查询结果进行筛选 |
| exclude() | 反选,排除满足条件的对象 |
| order_by(field) | 对QuerySets进行排序,(默认升序.`-field`降序,`?`随机) |
| reverse() | 反转排序 |
| distinct() | 去重,多表查询可能会用到 |
| values(*field) | 可以指定显示字段,QuerySet中以字典形式返回对象,形如[{x:'x'},{y:'y'},{z:'z'}] |
| values_list(*field) | QuerySet中以元组形式返回对象，形如[(x,'x'),(y,'y'),(z,'y')] |
| none() | 获取空的QuerySet |
| select_related() | 附带查询关联对象 |
| annotate() | 使用聚合函数 |
|  |  |
| **不返回全新QuerySet** |  |
| get() | 获取一个对象 |
| create() | 创建对象，无需save() |
| get_or_create() | 尝试查询对象，如果没有找到就新建对象,使用在post请求中 |
| update_or_create() | 尝试更新对象，如果没有找到就创建对象 |
| count() | 统计个数,永远不会引发异常 |
| latest() | 按日期返回最新对象 |
| earliest() | 按日期返回最旧对象 |
| first() | 返回QuerySet中第一个对象,默认按照主键排序的第一个 |
| last() | 返回QuerySet中最后一个对象,默认按照主键排序的最后一个 |
| exists() | 是判断对象是否存在最快的方式,返回一个bool值,存在为ture,不存在为false |
| update() | 更新 |
| delete() | 删除 |
| aggregate() | 聚合操作 |


关于**聚合函数**

导入方式`from django.db.models import *`

`aggregate()`:直接对整个QuerySet进行操作,结果只能是一条数据.
例如:`Article.objects.filter(Q(author=4)|Q(author=3) ).aggregate(num = Avg('score'))` 筛选出作者3和作者4得分的平均值.

`annotate()`:分组(group by)后在进行聚合操作,结果一般为多条数据.
例如:`Article.objects.values('author').annotate(Avg('score'))`按照作者分类,分别求出得分的平均值.

常用的聚合函数:`Avg`,`Count`,`Max`,`Min`,`Sum`


