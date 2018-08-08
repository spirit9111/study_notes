# Json web token (JWT)

### 什么是JWT?
Json web token (JWT), 是为了在网络应用环境间传递声明而执行的一种基于JSON的开放标准（(RFC 7519).该token被设计为紧凑且安全的，特别适用于分布式站点的单点登录（SSO）场景。JWT的声明一般被用来在身份提供者和服务提供者间传递被认证的用户身份信息，以便于从资源服务器获取资源，也可以增加一些额外的其它业务逻辑所必须的声明信息，该token也可直接被用于认证，也可被加密。

### 关于单点登录(SSO)
SSO的定义是在多个应用系统中，用户只需要登录一次就可以访问所有相互信任的应用系统.

### 为什么使用JWT
当只有一个server时完全可以使用session来保持登录状态(session保存在server),随着server增多进行负载均衡时,用户在访问同一个应用(网页),可能使用的server并不相同,server不同就导致了需要多次登录以便在多个server中记录session,不但体验不好而且需要数倍的空间保存同一个用户的登录状态.基于cookie还有可能遭遇CSRF攻击,相对于token不安全.

### token校验的流程

-用户使用用户名密码来请求服务器

-服务器进行验证用户的信息

-服务器通过验证发送给用户一个token

-客户端存储token，并在每次请求时附送上这个token值

-服务端验证token值，并返回数据

### JWT构成

头部(header)+载荷(payload)+签证(signature)
其中header和payload是base64加密,可以解密所以不能存放敏感信息
signature则是使用加密后的header+payload再进行一次根据secret_key加密,不能解密.
secret_key保存在server.

### 优点

-跨语言,jwt基于json

-体积小巧,便于传输

-payload可以解密,需要时可以保存不重要的信息


### django中使用
`pip install djangorestframework-jwt`
