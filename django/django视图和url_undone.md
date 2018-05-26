django的视图和url

对视图view的理解:
就是用来处理相应url页面请求的函数的集合(给定一个或者多个url寻找一个与之匹配的处理函数),执行函数返回请求的页面内容.

注意:筛选出来的url一定是--字符串(string)类型

一般习惯使用`views.py`来命名视图文件

视图至少需要一个参数`request`,用于接收HttpRequest对象

一个简单的视图
```python
from django.http import HttpResponse

def hello(request):
    return HttpResponse("Hello world")
```

对URLconf的理解:
路由,类似一个目录的功能,通过设置URLconf就能知道一个url请求调用那个函数来处理,可以设计多层路由来实现解耦.


`url(regex,view,kwargs,name)`

`url()`接收四个参数,其中`regex`,`view`必须有.

`regex`:表示正则表达式,需要注意的是用户请求的url地址会按照顺序匹配urlpatterns中的url()中的正则表达式,满足就不再执行,所以url顺序很重要.

`view`:处理对应满足正则的url地址的函数

`kwargs`:字典方式记录需要传递的参数给函数

`name`:对url命名,方便引用,相当于将url变成了全局变量让所有的文件都能访问到.







一个简单的URLconf
```python
from django.conf.urls import url
from . import views  # 通过当前文件夹导入views.py

urlpatterns = [
    url(r'^hello/$', views.hello),
    #  url
    ...
```

基本步骤:
1.先设置URLconf,关联url和函数
2.然后编写处理url请求的函数