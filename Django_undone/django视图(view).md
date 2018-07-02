# django视图(view) #

----------

视图层是django处理请求的**核心**代码层,
对外接收用户请求,接收**HttpRequest**对象
对内调度模型和模板,从数据库获取数据,经过逻辑判断处理好数据,发送给前端,返回给用户,返回**HttpResponse**对象.

一般用`views.py`命名视图函数的文件.
视图函数的一般形式:
```python
from django.http import HttpResponse
import datetime

def current_datetime(request):
    now = datetime.datetime.now()
    html = "<html><body>It is now %s.</body></html>" % now
    return HttpResponse(html)
```
`Http404`异常是一个可以认为抛出的异常,开启调试模式下,会使用内置的404模板.生产环境下则可以定制404.html的模板.
导入方式和用法
```python
from django.http import Http404
from django.shortcuts import render
from polls.models import Poll

def detail(request, poll_id):
    try:
        p = Poll.objects.get(pk=poll_id)
    except Poll.DoesNotExist:
        raise Http404("Poll does not exist")
    return render(request, 'polls/detail.html', {'poll': p})
```
类视图

----------


基本形式:
```python
from django.views.generic import View

class RegisterView(View):
    """类视图：处理注册"""

    def get(self, request):
        """处理GET请求，返回注册页面"""
        return render(request, 'register.html')

    def post(self, request):
        """处理POST请求，实现注册逻辑"""
        return HttpResponse('这里实现注册逻辑')
```

注册路由(as_view()):
`url(r'正则路由', views.RegisterView.as_view())`

对类视图进行装饰的一般用法:
1.`@method_decorator`方式
```python
# my_decorator自定义的装饰器
# name参数指定装饰的作用方法,
# dispatch表示该类视图所有的方式都被装饰
# 也可以单独指定get/post等

@method_decorator(my_decorator, name='dispatch')
class DemoView(View):
    def get(self, request):
        print('get方法')
        return HttpResponse('ok')

    def post(self, request):
        print('post方法')
        return HttpResponse('ok')

```

2.使用Mixin扩展类方式
```python
# Mixin扩展类需要继承自object
# 继承顺序-遵循类的多继承规律

class MyDecorator111Mixin(object):
    @classmethod
    def as_view(cls, *args, **kwargs):
        view = super().as_view(*args, **kwargs)
        view = my_decorator(view)
        return view

class MyDecorator222Mixin(object):
    @classmethod
    def as_view(cls, *args, **kwargs):
        view = super().as_view(*args, **kwargs)
        view = my_decorator(view)
        return view

class DemoView(MyDecoratorMixin, MyDecorator222Mixin,View):
    def get(self, request):
        print('get方法')
        return HttpResponse('ok')

    def post(self, request):
        print('post方法')
        return HttpResponse('ok')

```


3.路由方式,不推荐.


中间件(类似flask钩子)

----------
一般定义在`middleware.py`中,全局生效,在view函数前后进行操作.

需要注册到setting的`MIDDLEWARE`中生效,
如果有多个中间件生效,执行顺序为
前置钩子之上而下,后置钩子至下而上


一般形式,就是一个闭包函数
```python
def simple_middleware(get_response):
    # 此处编写的代码仅在Django第一次配置和初始化的时候执行一次。

    def middleware(request):
        # 此处编写的代码会在每个请求处理视图前被调用。

        response = get_response(request)

        # 此处编写的代码会在每个请求处理视图之后被调用。

        return response

    return middleware
```

