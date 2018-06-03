# django模型的增删改查 #

----------

## 增删改查操作: ##

## **查询:** ##

----------


查询数据表的所有内容,类似select * from ...
`model.objects.all()`

查询数据表中满足条件的内容,类似SQL的where,limit
`model.objects.filter(**kwargs)`

查询数据表中不满足条件的内容,相当于反选
`model.objects.exclude(**kwargs)`

查询一个满足条件的内容,get查出来的不是QuerySet,而是实例对象
`model.objects.get(**kwargs)`
当内容不存在(`DoesNotExist`) 
当内容多于一个(`MultipleObjectsReturned`) 

**查询的高级用法**

查询时对字段用`__`双下划线进行额外的限制(like,rlike,比较运算符)
`field__lookuptype=value`
常用参数:

| 参数 | 介绍 |对应的sql|
| --- | --- | --- |
| __gt/__gte | 大于/大于等于 | >/>= |
| __lt/__lte | 小于/小于等于 | </<= |
| __in | 在..之内的匹配 | in |
| __range | 范围匹配 | between...and |
| __exact | 默认值,条件严格区分大小写 | where |
| __iexact | 条件不区分大小写 | like |
| __contains | 包含条件,区分大小写 | like binary %xxx% |
| __icontains | 包含条件,不区分大小写 | like %xxx% |
| __date | 匹配日期,形如(2018,6,1) |  |
| __isnull | 判断是否为空 | is (not) null |
| __regex | 使用正则查询,区分大小写 | regex binary |
| __iregex | 使用正则查询,不区分大小写 | regex |
| __startswith/__endswith | 以什么开头/结尾,区分大小写 | rlike binary xx%/rlike binary %xx |
| __istartswith/__iendswith | 以什么开头/结尾,不区分大小写 | rlike xx%/rlike %xx |


## 跨关系表查询 ##
(inner join...on...)

跨关系单值(只有一个条件或者是and连接的条件)查询:
**objects前面用的是哪个class，返回的就是哪个class的对象。**
`models.object.filter(关联models(必须用小写)__field__lookuptype = value)`

跨关系多值(逻辑关系复杂,使用普通的filter容易造成混乱)查询:
使用Q查询来简化复杂的逻辑关系.
形如:
`models.object.exclude(Q(models__field__lookuptype = value) | Q(models__field__lookuptype = value) & ~Q(field__lookuptype = value))`


## 关于Q对象 ##

使用Q查询,必须先导入`from django.db.models import Q`
Q()对象必须放置在普通的关键字参数前面.

`&`与,相当于sql中的`and`
`|`或,相当于sql中的`or`
`~`非,相当于sql中的`!`

```
Poll.objects.get(
Q(question__startswith='Who'),
Q(pub_date=date(2005, 5, 2)) | Q(pub_date=date(2005, 5, 6))
)
# 它相当于
# SELECT * from polls WHERE question LIKE 'Who%'
AND (pub_date = '2005-05-02' OR pub_date = '2005-05-06')
```
## 关于F对象 ##

使用F查询,必须先导入`from django.db.models import F`
F()对象可以进行加、减、乘、除、取模以及幂运算等算术操作
F()常常用在同一张表内的两个字段进行比较/计算,比如日期计算,赞数和踩数进行比较等.

## 反向关联 ##
默认情况下:

**一对多**.Amodel为一,Bmodel为多(ForeignKey)
如果已知Amodel的模型的实例`a`,可以通过`a.bmodel_set.all()`来查询Bmodel中的有关a的所有数据(加上了`_set`)
如果已知Bmodel的模型实例`b`,可以通过`b.amodel`来查询数据(amodel就是Bmodel中的一个字段而已)

**多对多**.Cmodel(ManyTOMany设置在Cmodel),Dmodel
如果已知Cmodel的实例`c`,可以通过`c.dmodels.all()`来查询Dmodel中有关c的全部内容.(加上了`s`仔细看)
如果已知Dmodel的实例`d`,可以通过`d.cmodel_set.all()`来查询Cmodel中有关d的全部内容.(加上了`_set`)


## **增加:** ##

----------


增加数据(相当于SQL的insert语句):
```
# 第一种方式,创建和保存分开操作
a = models(field1 = xxx, field2 = yyy, ...)
a.save()  

# 第二种方式,创建保存一步进行
models.object.create(field1 = xxx, field2 = yyy, ...)

# 第三种方式,先创建实例然后设置属性
b = models()
b.field1=xxx
b.field2=yyy
...
b.save()

# 第四种方式,尝试创建数据,不能存在就创建,存在就失败(object, True/False)
models.objects.get_or_create(field1="xxx, field2=yyy)

```

## **修改:** ##

----------


修改一条数据(相当于SQL的update语句)和增加操作一样
```
a = models.object.get()
a.field1 = xxx 
a.field2 = yyy 
a.save()
```

批量修改数据,会把满足条件的字段内容全部修改
**危险操作**
```
# 名称中包含 "abc"的人 都改成 xxx
models.objects.filter(name__contains="abc").update(name='xxx') 
```
**注意**
update()方法会立即执行但不会立即save(),如果想要更新后保存需要使用for循环

## **删除:** ##

----------

从数据库中删除数据(**危险操作**)
```
# 删除一条数据
models.object.get(xxx).delete()

# 删除多条数据
models.object.filter(xxx).delete()

# 删除所有记录
models.objects.all().delete() 
```
