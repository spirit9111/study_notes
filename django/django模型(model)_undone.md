# django模型(model) #

----------

## 模型 ##

本质上就是一个通过type元类来实现的特殊的python类class(都是django.db.models.Model的子类)
核心思想就是ORM(“Object Relational Mapping”，即对象-关系-映射).
实现了对数据库功能封装,让python和数据库操作解耦.

![ORM-pymysql](https://i.imgur.com/EQ25KZG.png)

简单来看就是将这个特殊的class与数据库进行映射关联

类名--->table(table_name为自动生成,形式为app_name + '_' +class_name)

类属性--->字段(列)

实例--->数据(行)

简单的创建步骤:创建模型(在models.py中创建,继承models.Model),将模型所在的app名称安装到INSTALLED_APPS(在settings.py中设置)


## 字段fields ##
django字段对应的就是数据库中的字段,类属性就是数据表的字段名

字段的命名规则:

1.不能与python的关键字重名

2.不能使用双(多个)连续的下划线(`__`,`___`等)

常用字段类型

|    常用类型  | 说明 |
| ---------- | --- |
| CharField |  字符串类型。必须接收一个max_length参数，表示字符串长度不能超过该值。默认的表单标签是input text。最常用的filed，没有之一！ |
| IntegerField | 整数类型，最常用的字段之一。取值范围-2147483648到2147483647。在HTML中表现为NumberInput标签。 |
| BooleanField | 布尔值类型。默认值是None。在HTML表单中体现为CheckboxInput标签。如果要接收null值，请使用NullBooleanField。 |
| TextField | 	大量文本内容，在HTML中表现为Textarea标签，最常用的字段类型之一！如果你为它设置一个max_length参数，那么在前端页面中会受到输入字符数量限制，然而在模型和数据库层面却不受影响。只有CharField才能同时作用于两者。 |
| DateField       |  class DateField(auto_now=False, auto_now_add=False, **options)日期类型。一个Python中的datetime.date的实例。在HTML中表现为TextInput标签。在admin后台中，Django会帮你自动添加一个JS的日历表和一个“Today”快捷方式，以及附加的日期合法性验证。两个重要参数：（参数互斥，不能共存） auto_now:每当对象被保存时将字段设为当前日期，常用于保存最后修改时间。auto_now_add：每当对象被创建时，设为当前日期，常用于保存创建日期(注意，它是不可修改的)。设置上面两个参数就相当于给field添加了editable=False和blank=True属性。如果想具有修改属性，请用default参数。例子：pub_time = models.DateField(auto_now_add=True)，自动添加发布时间。 |
| DateTimeField | 日期时间类型。Python的datetime.datetime的实例。与DateField相比就是多了小时、分和秒的显示，其它功能、参数、用法、默认值等等都一样。 |
| EmailField | 邮箱类型，默认max_length最大长度254位。使用这个字段的好处是，可以使用DJango内置的EmailValidator进行邮箱地址合法性验证。 |
| GenericIPAddressField | class GenericIPAddressField(protocol='both', unpack_ipv4=False, **options)[source],IPV4或者IPV6地址，字符串形式，例如192.0.2.30或者2a02: 42fe::4在HTML中表现为TextInput标签。参数protocol默认值为‘both’，可选‘IPv4’或者‘IPv6’，表示你的IP地址类型。 |
| FileField | class FileField(upload_to=None, max_length=100, **options)上传文件类型,upload_to 指定上传的路径 |
| ImageField | 图像类型 |
| URLField | 一个用于保存URL地址的字符串类型，默认最大长度200。 |
| UUIDField | 用于保存通用唯一识别码（Universally Unique Identifier）的字段。使用Python的UUID类。在PostgreSQL数据库中保存为uuid类型，其它数据库中为char(32)。这个字段是自增主键的最佳替代品 |

关系型字段:

第一个参数为

一对一:
使用`models.OneToOneField(to,on_delete)`来设置,常用于对原模型功能进行拓展(相当于是),

一对多

多对多












对models增/删/改操作基本步骤:

1.在models.py中增/删/改models

2.将对models的增/删/改操作,创建到migrations(概念和git中的add类似)
`python manage.py makemigrations`

3.提交增/删/改操作到的数据表(正式提交生效,与git的commit类似)
`python manage.py migrate`

migrate命令和git命令的思路十分相似,migrations相当于git的缓存区的概念,通过记录跟踪`改变的操作`,用新/旧对比的方式,来完成相应修改操作.

显示出migrations对应的sql语句
`python manage.py sqlmigrate app_name num`

如果重写了生成的migrations可以用进行检查
`python manage.py check`


增删改查操作:

查询:

查询数据表的所有内容,类似select * from ...
`model_name.objects.all()`

查询数据表中满足条件的内容,类似where
`model_name.objects.filter(条件)`

查询一个满足条件的内容
`model_name.objects.get(条件)`






增/改:


删除:



