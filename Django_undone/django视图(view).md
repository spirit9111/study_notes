# django视图(view) #

----------

视图层是django处理请求的**核心**代码层,
对外接收用户请求,接收**HttpRequest**对象
对内调度模型和模板,从数据库获取数据,经过逻辑判断处理好数据,发送给前端,返回给用户,返回**HttpResponse**对象.

一般用`views.py`命名视图函数的文件.

HttpRequest
HttpResponse