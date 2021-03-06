# CSRF简单小结 #

----------

CSRFProtect 相关设置

form表单中设置csrf_token保护
```
<input type="hidden" name="csrf_token" value="{{ csrf_token() }}"/>
```


ajax请求是headers中带上csrf_token
```
headers: {
    "X-CSRFToken": getCookie("csrf_token")
},
```
后端接收请求后,给每一个请求cookie中添加csrf_token
```
@app.after_request
def after_request(response):
    # 调用函数生成 csrf_token
    csrf_token = generate_csrf()
    # 通过 cookie 将值传给前端
    response.set_cookie("csrf_token", csrf_token)
    return response
```




CSRF是什么?CSRF有什么用处?
CSRF(Cross Site Request Forgery),跨站请求伪造.
简单来说就是黑客可以通过CSRF冒用你的身份,在网站上进行了没有经过你允许的特殊操作(恶意操作),比如转账/购买等.

CSRF攻击实现的原理:

![](https://i.imgur.com/3ijPL5D.png)

在**没有**开启CSRF保护的前提下

1.在客户登录网站A(正规)时,会提交相关的数据用于验证身份.

2.网站A的服务器在验证通过后会将cookie信息随着response返回给客户的浏览器(cookie保存在客户的浏览器上),以便实现状态保持功能.

3.如果此时客户在没有登出(**清除cookie/cookie过期**,关闭浏览器**不能**清除cookie)网站A的前提下,又访问了网站B(非正规/黑客)并且操作了带有CSRF攻击功能的程序.

4.网站B就会在客户**不知晓**的情况下,跳转到网站A的某些功能页面(比如转账)并提交相应的数据,**以客户的名义**发送请求(网站A只能靠cookie判断客户身份,此时cookie依然有效能在网站A验证通过,网站A仍然认为是客户在进行操作),网站A就会在客户请求通过后进行相应的处理.

5.网站B就成功的利用CSRF完成了攻击.(网站B至始至终都没有**获取**到客户的cookie,因为cookie是保存在客户的浏览器上的,浏览器的**同源原则**)


CSRF攻击防护:

总结上面的CSRF攻击的原理,CSRF问题的关键就是仅仅验证一般的cookie不够安全的.

这是就需要使用到**csrf_token** ,csrf_token其实就是一段动态生成的随机数.
每一次请求发生都会发生变化.

当客户发起登录请求时,服务器给客户返回cookie上设置csrf_token,
在返回给客户的网页上(比如form表单中)也加入相同的csrf_token(隐藏的).

当客户提交请求时,服务器先从cookie获取csrf_token,再从表单中获取csrf_token,进行比对,通过才能进行下一步的操作.

而当黑客进行CSRF攻击时,伪造的数据中时没有办法获取隐藏在页面上的csrf_token的,发送请求时只有以客户名义自动发送的cookie中的csrf_token不能完成验证.
