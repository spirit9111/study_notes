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


## view中常用的方法/函数: ##

**render()/渲染**
`render(request, template_name, context=None, content_type=None, status=None, using=None)`
作用是将一个字典中的数据按照指定的模板进行渲染,最后返回一个HttpResponse对象.
常用参数:
`request`:必选,其实就是view函数的request,包含了请求头的全部内容.
`template_name`:必选,渲染用的一个模板(template),可以接收模板的列表但只会使用第一个模板.
`context`:可选,包含数据的字典.
`status`:可选,响应头的状态码.默认为200.
```python
from django.shortcuts import render

def my_view(request):
    # View code here...
    return render(request, 'myapp/index.html', 
    {'foo': 'bar'},
     content_type='application/xhtml+xml')
```
**redirect()/重定向**
`redirect(to, permanent=False, args, *kwargs)`
作用:重定向,接收一个url,返回一个HttpResponseRedirect.
常用参数:
`to`:一个用于重定向的目标url地址,可以是model查询出的url数据,自动反解析出url/或者是url的name,自动反解析出url/或者直接是一个url地址.
`permanent`:用于设置是否是永久重定向.(True/False)

**get_object_or_404()**
`get_object_or_404(klass, args, *kwargs)`
**非常强大而且常用的方法.**
作用:搜索一个对象,如果有则继续,否则弹出404.
常用参数:
`klass`:模型名(或是queryset)和条件,指定从哪个模型按照哪个条件进行查找.

**get_list_or_404()**
`get_list_or_404(klass, args, *kwargs)`
作用/参数/用法基本和`get_object_or_404`一样,
最终的结果是一个包含一个或多个对象list,必须有对象,如果为空就会404异常.


HttpRequest对象

HttpRequest也就是view接收到的第一个参数request,HttpResponse包含了非常多的数据.(大部分是只读)
**常用属性:**

| 属性 | 介绍 | 数据类型 |
| --- | --- | --- |
| .scheme | 协议种类,http/https | 字符串 |
| .**body** | 原始的请求体的正文,常用用于处理二进制图像 | bytes二进制 |
| .**path** | 请求页面的路径,不包含域名. | 字符串 |
| .**path_info** | 基本和.path一样,可以适应一些特殊的web-server | 字符串 |
| .**method** | 分辨http的请求方式(GET/POST等),默认是大写 | 字符串 |
| .encoding | 提交的数据的编码方式,**可重写** | 字符串 |
| .**GET** | 包含get请求的全部参数(url中?后面的一串数据) | QueryDict对象,类似字典 |
| .**POST** | 包含post请求的全部参数(.body的一部分)和表单数据的字典(主要) | QueryDict对象,类似字典 |
| .**COOKIES** | 包含所有Cookie信息的字典 | 字典(key-value都为字符串) |
| .**FILES** | 包含上传文件的数据,上传文件必用 | 类似于字典的对象 |
| .META | 包含HTTP头部信息的字典 | 字典(大写且以`HTTP_`开头,用`_`连接) |

**常用方法:**

| 方法 | 介绍 |  |
| --- | --- | --- |
| .get_host() | 获取请求的原始主机 |  |
| .get_port() | 获取原始的端口 |  |
| .get_full_path() | 获取完整的url地址,包含get中?及后面的内容 |  |
| .get_signed_cookie(key, default=RAISE_ERROR, salt='', max_age=None) | 从cookie中获取值,可以加盐提高安全系数 |  |
| .is_secure() | 判断是否是Https，是则为True |  |
| .is_ajax() | 判断是否是ajax请求,是则为ture |  |
|  |  |  |
|  |  |  |
|  |  |  |













HttpResponse
HttpResponseNotFound
HttpResponseRedirect