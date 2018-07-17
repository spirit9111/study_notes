django项目配置一般步骤


1.创建项目
`django‐admin startproject project_name`

2.创建应用
`python manage.py startapp`

3.注册应用
setting下的`INSTALLED_APPS`中进行设置

4.创建视图
应用下的`view.py`中设置

5.注册路由
5.1在应用中新建`urls.py`当做二级路由
5.2在项目中`urls.py`中的总路由中配置

6.配置静态文件(debug模式生效)
6.1设置static
```
#在setting中新增

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR, 'static'),
]
```
6.2设置templates
```
#根路径下新建 templates文件夹
#在setting中的TEMPLATES设置模板路径

'DIRS': [os.path.join(BASE_DIR, 'templates')],
```

7.配置redis存储session
7.1安装redis:`pip install django-redis`
7.2setting中新增(如果redis不在本地,需要修改redis中的bind配置)
```python
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/0",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
SESSION_ENGINE = "django.contrib.sessions.backends.cache"
SESSION_CACHE_ALIAS = "default"
```


8.配置数据库(mysql为例)
8.1安装pymysql`pip install PyMySQL`
8.2配置相关
```python
# __init__.py中设置
from pymysql import install_as_MySQLdb

install_as_MySQLdb()

#修改数据库配置
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': '数据库名字',
        'HOST': '数据库ip',
        'USER': 'root',
        'PASSWORD': 'pwd',
        'PORT': '3306',
    }
}
```
8.3 新建数据库


其他设置:

```
LANGUAGE_CODE = 'zh-hans'
TIME_ZONE = 'Asia/Shanghai'
```