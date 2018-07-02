# Django中的cookie和session #

----------
Cookie

----------


一般设置方式(response中设置):
```python
HttpResponse.set_cookie(cookie名, value=cookie值, max_age=cookie有效期)

或者

response = HttpResponse('ok')
response.set_cookie('itcast2', 'python2', max_age=3600)  # 有效期一小时
```

获取方式(request中获取):
`request.COOKIES.get('cookie_name')`

Session

----------
存储方式:
1.数据库中,默认方式
`SESSION_ENGINE='django.contrib.sessions.backends.db'`
2.本地缓存
`SESSION_ENGINE='django.contrib.sessions.backends.cache'`
3.混合存储
`SESSION_ENGINE='django.contrib.sessions.backends.cached_db'`
4.redis(需要安装django-redis)
redis配置:
```
CACHES = {
    "default": {
        "BACKEND": "django_redis.cache.RedisCache",
        "LOCATION": "redis://127.0.0.1:6379/1",
        "OPTIONS": {
            "CLIENT_CLASS": "django_redis.client.DefaultClient",
        }
    }
}
SESSION_ENGINE = "django.contrib.sessions.backends.cache"
SESSION_CACHE_ALIAS = "default"
```

获取及操作方式:


```python
1） 以键值对的格式写session。

request.session['键']=值

2）根据键读取值。
request.session.get('键',默认值)

3）清除所有session，在存储中删除值部分。
request.session.clear()

4）清除session数据，在存储中删除session的整条数据。
request.session.flush()

5）删除session中的指定键及值，在存储中只删除某个键及对应的值。
del request.session['键']

6）设置session的有效期
request.session.set_expiry(value)
```