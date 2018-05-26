初识django

环境
python3.6.5
django1.11

几个常用命令

创建一个名为project_name的django项目
`django‐admin.py startproject project_name`

运行django开发服务器(http://127.0.0.1:8000/)
`python manage.py runserver`

创建一个名为app_name的app应用
`python manage.py startapp app_name`

启动django的python-shell(自动调用django的settings)
`python manage.py shell`

生成migrations文件
`python manage.py makemigrations`

提交生成的migrations文件
`python manage.py migrate`










django设置相关内容--settings.py


设置北京时间为准(东八区)

`TIME_ZONE = 'Asia/Shanghai'` 

注册自定义的app

````
INSTALLED_APPS = [
    'polls.apps.PollsConfig',
    ...
]
```

数据库的配置(mysql为例)

```python
import pymysql
pymysql.install_as_MySQLdb()

DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'mysite',
        'HOST': '192.168.1.1',
        'USER': 'root',
        'PASSWORD': 'pwd',
        'PORT': '3306',
    }
}
```









注意： Django的开发服务器具有自动重载功能，当你的代码有修改，每隔一段时间服务器将自动更新.


include语法相当于多级路由，它把接收到的url地址去除前面的正则表达式，将剩下的字符串传递给下一级路由进行判断。

django的view

django中的view就是第一个简单的python函数

一个请求页面
一个处理页面的函数
通过urls关联
轮询匹配
匹配成功就将请求地址返回给函数当做参数
调用函数处理请求
返回处理结果

