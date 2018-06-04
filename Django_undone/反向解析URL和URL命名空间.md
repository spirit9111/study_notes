# 反向解析URL和URL命名空间 #

----------

首先明确几个概念:
1.在html页面上的内容特别是向用户展示的url地址,比如常见的超链接,图片链接等,最好能动态生成,而不要固定.
2.一个django项目中一般包含了多个django应用(app).
3.一个视图(view)往往对应多个url地址.


在django中实现反向解析URL必备条件就是**url和view能一对一**的匹配.
(通过view找到唯一一个对应的url,通过url也能找到唯一一个view)

最**简单的方式**就是使用`name`,可以理解为url起了一个名字.
例如:
```
from django.conf.urls import url
from . import views

urlpatterns = [
    #...
    url(r'^articles/([0-9]{4})/$', views.year_archive, name='news-year-archive'),
    #...
]
```
此时的`news-year-archive`就可以表示`/articles/nnnn/`在view中进行使用.

在templates中使用
```
<a href="{% url 'news-year-archive' 2012 %}">2012 Archive</a>
```

在view中使用
```
from django.urls import reverse
from django.http import HttpResponseRedirect

def redirect_to_year(request):
    # ...
    year = 2006
    # ...
    return HttpResponseRedirect(reverse('news-year-archive', args=(year,)))
```
但是使用`name`也存在一定的**问题**,比如在同一个项目中的不同的app中`name`可能会重名(导致反解析时一个view对应多个url),而且给每一个url起不同名字也很繁琐.

这时候就会用到**URL命名空间**
URL命名空间包括两个部分:`app_name`(**应用命名空间**)以及`namespace`(**实例命名空间**)

对于`app_name`官方解释"它表示正在部署的应用的名称。一个应用的每个实例具有相同的应用命名空间。",比较好理解.
也就是说可以通过设置`app_name`来区分不同app中同名的`name`了,使用`:`连接.

但是对于`namespace`官方解释"它表示应用的一个特定的实例。**实例的命名空间**在你的全部**项目中**应该是**唯一**的。但是，一个实例的命名空间可以和应用的命名空间相同。",就比较的难以理解.

`namespace`主要功能为了区分同一个app下不同实例,使得反解析url时能获得正确的结果.

例如:
在不加入`namespace`时,
访问`http://127.0.0.1:8000/ccc/aaa/`和`http://127.0.0.1:8000/bbb/aaa/`
结果均为`/ccc/aaa/`,这显然不是我们想要获取的结果.

```
# 主url.py
urlpatterns = [
    ...
	url(r'^bbb/', include("test_namespace2.urls")),
	url(r'^ccc/', include("test_namespace2.urls")),
    ...
]

# test_namespace2/url.py
app_name = "app02"

urlpatterns = [
    url(r'aaa/$', views.aaa, name="index"),
]

# test_namespace2/view.py
def aaa(request):
	return HttpResponse(reverse("app02:index"))

```

做出一些修改,加入`namespace`用作区别
```
# 主url.py
urlpatterns = [
    ...
	url(r'^bbb/', include("test_namespace2.urls", namespace='bbb')),  # 加入了namespace
	url(r'^ccc/', include("test_namespace2.urls", namespace='ccc')),
    ...
]

# test_namespace2/view.py
def aaa(request):
	return HttpResponse(reverse("app02:index", current_app=request.resolver_match.namespace))  # 使用namespace
```
这样就会获得正确的结果了.

----------

使用方式:

首先在,主url.py中添加`namespace`
```
urlpatterns = [
    url(r'^polls/', include('polls.urls',namespace='test')),
]
```
然后要在app的urls.py中添加`app_name`和`name`
比如:
```
app_name = 'polls'
urlpatterns = [
    #...
    url(r'^$', views.index, name='index'),
    #...
```

然后在view和templates中使用了,此时就算有多个app中都有名为`index`的`name`也不会有问题了
使用方式,使用形如`app_name:name`
在view中使用:
```
reverse('polls:index', current_app=request.resolver_match.namespace)
```
在templates中使用
```
{% url 'polls:index' %}
```





