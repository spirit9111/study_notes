# django模型的增删改查 #

----------

## 增删改查操作: ##

**查询:**

查询数据表的所有内容,类似select * from ...
`model.objects.all()`

查询数据表中满足条件的内容,类似SQL的where
`model.objects.filter(条件)`

查询数据表中不满足条件的内容,相当于反选
`model.objects.exclude(条件)`

查询一个满足条件的内容
`model.objects.get(条件)`

值的注意的是:

1.使用get方法时当1.内容不存在(`DoesNotExist`) 或者 2.内容多于一个(`MultipleObjectsReturned`) 都会报错.

2.filter和exclude返回对象都是QuerySets对象,可以理解为python中的list,可以迭代/循环/获取索引/切片(不支持负索引)

3.QuerySets是**惰性**的操作,只有进行**evaluated**操作时才会真正的连接数据库进行查询操作,目的是 对查询进行优化 提高数据库查询效率，减少操作次数.




**增加:**

增加数据(相当于SQL的insert语句):
```
# 第一种方式,创建和保存分开操作
a = models(field1 = xxx, field2 = yyy, ...)
a.save()  
# 第二种方式,创建保存一部进行
models.object.create(field1 = xxx, field2 = yyy, ...)
```

**修改:**

修改某条数据(相当于SQL的update语句)
```
a.field = zzz  # 对于一般字段,zzz表示一般的数据
a.field = b  # 对于外键约束的字段,b必须是关联字段的数据
a.save()

a.field.add(c)  # 对于多对对字段,需要额外使用add(),c表示关联字段的数据
```
`save()`用于保存普通字段和外键字段

`add()`用于保存多对多的字段,不需要再次调用save()

**删除:**



