# flask基础-视图/路由 #

----------


Flask有两大核心：Werkzeug和Jinja2

- Werkzeug实现路由、调试和Web服务器网关接口
- Jinja2实现了模板。

## 创建flask项目的基本步骤 ##
1.导入flask模块,
`from flask import Flask`
2.创建app对象
`app = Flask(__name__)`
3.创建视图函数及相应的路由规则
```python
@app.route('/')  # 路由规则
def index():  # 视图函数
	return 'hello flask'
```
4.启动web服务器
```python
if __name__ == '__main__':
    # 运行,支持参数(host="x.x.x.x", port=x, debug = True)
	app.run() 
```

## 创建app对象常用的参数: ##
```
def __init__(self, import_name, static_path=None, static_url_path=None,static_folder='static', template_folder='templates',instance_path=None, instance_relative_config=False):
pass
```

| 常用参数 | 介绍 |
| --- | --- |
| import_name | 决定Flask在访问静态文件时查找的路径,一般使用__name__来指定为当前包(模块) |
| static_url_path | 静态文件的访问地址,默认为 |
| static_folder | 静态文件的储存地址,默认为static |
| template_folder | 模板文件储存地址,默认为templates |


## 路由以及视图基础 ##

获取url中的部分数据,并传递给视图
一般形式,使用`<变量名>`来获取数据,类型为字符串
```python
@app.route('/user/<user_id>') # 使用变量来保存需要的数据

def user_info(user_id):  # 需要接收变量
    return 'hello %s' % user_id
```

限制路由的请求方式:(methods)
`@app.route('/demo2', methods=['GET', 'POST'])`
常用的请求方式:

| HTTP请求方式 | 介绍 |
| --- | --- |
| GET | 向服务器请求页面,并返回响应头和响应体 |
| POST | 提交数据给服务器, |
| HEAD | 类似GET,但是只返回响应头 |
| OPTIONS | 请求服务器返回支持的所有HTTP请求方法,自动判断需要的请求方式 |
| PUT | 向指定资源位置上传更新的全部内容 |
| PATCH | 类似put,但是只会更新修改过的部分 |
| DELETE | 用于请求服务器删除所请求URI,请求后指定资源会被删除 |


**正则匹配及转换器**

转换器的作用:

定义转换器可以在的多个视图函数中进行复用,减少代码冗余.

默认转换器
```
DEFAULT_CONVERTERS = {
    'default':          UnicodeConverter,
    'string':           UnicodeConverter,
    'any':              AnyConverter,
    'path':             PathConverter,
    'int':              IntegerConverter,
    'float':            FloatConverter,
    'uuid':             UUIDConverter,
}
```

自定义转换器的步骤:
1.导入转换器基类
`from werkzeug.routing import BaseConverter`
基类BaseConverter的源码
```python
class BaseConverter(object):

    regex = '[^/]+'
    weight = 100

    def __init__(self, map):
        self.map = map

    def to_python(self, value):
        return value

    def to_url(self, value):
        return url_quote(value, charset=self.map.charset)
```

2.自定义转换器
```python
class RegexConverter(BaseConverter):  # 定义转换器RegexConverter并继承基类
    def __init__(self, url_map, *args):  # 对父类的init方法进行扩展,使之能接收参数,
        super(RegexConverter, self).__init__(url_map)  # 
        self.regex = args[0]   # 接收参数中新的正则规则,并重写regex类属性
```
3.将自定义转换器,注册到转换器字典`DEFAULT_CONVERTERS`中
`app.url_map.converters['re'] = RegexConverter`

4.调用转换器处理url
```python
@app.route('/user/<re("[0-9]{3}"):user_id>')
def user_info(user_id):
    return "user_id 为 %s" % user_id
```

转换器方法:
to_python:在url进行正则匹配后对满足条件的url中需要记录的数据进行处理,然后传给是视图函数,比如

to_url:在url进行匹配正则之前,对url中的数据进行处理,然后在进行正贼规则的匹配.


`url_map`:用于记录路由规则和视图函数的对应关系

`url_for`:根据函数名反向生成url,使用url_for生成指定视图函数所对应的url


视图函数**返回JSON格式**数据的方式:`jsonify()`
直接将字典转换为JSON返回客户端
```python
@app.route('/demo4')
def demo4():
    # 定义字典
    json_dict = {
        "user_id": 10,
        "user_name": "laowang"
    }
    # 使用flask中的jsonify方法,将字典转换为JSON格式
    return jsonify(json_dict)
```

视图函数**重定向**的方法:`redirect()`
```python
@app.route('/demo5')
def demo5():
    # 重定向到指定url
    return redirect('www.baidu.com')

    # 重定向到已定义的视图函数
    # return redirect(url_for('demo1'))
```

视图函数**自定义状态码**方法
```python
@app.route('/demo6')
def demo6():
    return 'response', status
```

Flask加载配置的方法:
所谓配置就是开启一些特殊功能,如debug模式,连接数据库
1.从配置对象加载(主要方式)`app.config.form_object()`
```
# 创建配置对象,
class Config(object):
    DEBUG = True
    ...

# 加载配置对象
app.config.from_object(Config)
...
```

2.从配置文件加载(主要方式)`app.config.form_pyfile()`
```
# 需要先创建config.ini文件,写入相关配置

# 从配置文件中加载配置
app.config.from_pyfile('config.ini')
```

3.从环境变量加载`app.config.from_envvar()`

抛出异常和捕获异常

`abort`主动抛出状态码和指定的异常,状态码必须为HTTP协议中的种类,不支持自定义状态码.
```
abort(404)

abort(ZeroDivisionError)
```

`errorhandler`装饰器,捕获异常处理异常
```
@app.errorhandler(500)
def internal_server_error(e):
    return '服务器搬家了'

@app.errorhandler(ZeroDivisionError)
def zero_division_error(e):
    return '除数不能为0'
```

请求钩子:能在视图函数执行前后进行相关的处理,比如权限验证,连接数据库的操等.
`@before_first_request`:第一次处理请求前执行,也就是第一次进入视图函数前
`@before_request`:每次请求前都要执行,
`@after_request`:请求结束后执行,接受一个响应,在发送响应前进行最后一次处理,并返回response
`@teardown_request`:每次请求后执行,接受一个错误,并抛出.


request对象

常用属性

|  属性  |  说明	|  类型  |  
| --- | --- | --- | ---  | 
|  data	|  记录请求的数据，并转换为字符串	|  *  |  
|  **form**	|  记录请求中的表单数据	|  MultiDict  |  
|  **args**	|  记录请求中的查询参数	|  MultiDict  |  
|  **cookies** |  	记录请求中的cookie信息	|  Dict  |  
|  headers	|  记录请求中的报文头	|  EnvironHeaders  |  
|  **method**	|  记录请求使用的HTTP方法	|  GET/POST  |  
|  **url**	|  记录请求的URL地址|  string  |  
|  **files**	|  记录请求上传的文件	|  *  |  



状态保持方式:


## Cookie ##
指某些网站为了辨别用户身份、进行会话跟踪而储存在用户本地的数据（通常经过加密）

特点:
1.cookie数据保存在客户端,是纯文本文件,不够安全,不能保存敏感信息
2.cookie由服务器生成,跟随着response,以key-value形式,返回给客户端
3.cookie基于域名安全,不同域名之间的cookie不能相互访问.

应用场景:验证登录状态,广告推送,购物车

cookie设置方式(服务器):`set_cookie()`
```python
from flask imoprt Flask,make_response
@app.route('/cookie')
def set_cookie():
    resp = make_response('this is to set cookie')
    resp.set_cookie('username', 'xxxx', max_age=3600)  # max_age设置cookie的过期时间,单位是秒
    return resp
```
cookie获取方式(服务器):`request.cookies.get()`
```python
from flask import Flask,request
#获取cookie
@app.route('/request')
def resp_cookie():
    resp = request.cookies.get('username')
    return resp
```

cookie流程:
![](https://i.imgur.com/iDHBjhz.png)


## Session: ##
对于敏感信息需要使用session保存到服务器

特点:
session数据保存在服务器
session依赖于cookie机制
设置session后,会自动把加密后的cookie返回给客户端

session设置/获取/删除方式:
```python
1.设置secret_key(加盐)
第一种形式:app.secret_key = 'xxxx' 
第二种方式:app.config['secret_key']='xxxx'

# 登录,设置session
@app.route('/login')
def login():
    session['username'] = 'xxxx'
    session['password'] = 'yyyy'
    return 'success'

# 获取session时,如果没有设置为空
@app.route('/')
def index():
    result = session.get('username','')
    return result

# 登出,删除session
@app.route('/logout')
def logout():
    session.pop('username')
    return 'success'

```


请求上下文(request context):request,session

应用上下文(application context):current_app,g变量


Flask常用扩展包：

Flask-SQLalchemy：操作数据库；
Flask-script：插入脚本；
Flask-migrate：管理迁移数据库；
Flask-Session：Session存储方式指定；
Flask-WTF：表单；
Flask-Mail：邮件；
Flask-Bable：提供国际化和本地化支持，翻译；
Flask-Login：认证用户状态；
Flask-OpenID：认证；
Flask-RESTful：开发REST API的工具；
Flask-Bootstrap：集成前端Twitter Bootstrap框架；
Flask-Moment：本地化日期和时间；
Flask-Admin：简单而可扩展的管理接口的框架