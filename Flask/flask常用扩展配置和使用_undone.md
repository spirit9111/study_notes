flask常用扩展配置和使用

----------


**redis数据库**

----------
```
import redis

redis_store = redis.StrictRedis()

**Flask-SQLalchemy**：操作数据库；
```
----------
```
from flask_sqlalchemy import SQLAlchemy

SQLALCHEMY_DATABASE_URI = "mysql://root:mysql@127.0.0.1:3306/information"
SQLALCHEMY_TRACK_MODIFICATIONS = False

db = SQLAlchemy(app)
```
**Flask-script**：插入脚本；

----------
```
from flask_script import Manager

manager = Manager(app)

manager.run()
```

**Flask-migrate**：管理迁移数据库；

----------
```
from flask_migrate import Migrate, MigrateCommand

migrate = Migrate(app)
Migrate(app, db)
manager.add_command('db', MigrateCommand)
```

Flask-Session：Session存储方式指定；

----------
```
from flask_session import Session

SESSION_TYPE = "redis" # 指定 session 保存到 redis 中
SESSION_USE_SIGNER = True # 让 cookie 中的 session_id 被加密签名处理
SESSION_REDIS = redis.StrictRedis() # 使用 redis 的实例
PERMANENT_SESSION_LIFETIME = 86400 # session 的有效期，单位是秒

session = Session(app)
```
**Flask-WTF**：表单；

----------
```
#开启csrf保护
from flask_wtf.csrf import CSRFProtect

csrf = CSRFProtect(app)
```
**Flask-Mail**：邮件；

----------

Flask-Bable：提供国际化和本地化支持，翻译；

----------

**Flask-Login**：认证用户状态；

----------

Flask-OpenID：认证；

----------

Flask-RESTful：开发REST API的工具；

----------

**Flask-Bootstrap**：集成前端Twitter Bootstrap框架；

----------

**Flask-Moment**：本地化日期和时间；

----------

**Flask-Admin**：简单而可扩展的管理接口的框架

----------

**Flask-PageDown**:MarkDown语法
```
from flask_pagedown import PageDown

pagedoen = PageDown(app)
```



日志相关配置

----------
```
# 设置日志的记录等级
logging.basicConfig(level=logging.DEBUG) # 调试debug级

# 创建日志记录器，指明日志保存的路径、每个日志文件的最大大小、保存的日志文件个数上限
file_log_handler = RotatingFileHandler("logs/log", maxBytes=1024*1024*100, backupCount=10)

# 创建日志记录的格式 日志等级 输入日志信息的文件名 行数 日志信息
formatter = logging.Formatter('%(levelname)s %(filename)s:%(lineno)d %(message)s')

# 为刚创建的日志记录器设置日志记录格式
file_log_handler.setFormatter(formatter)

# 为全局的日志工具对象（flask app使用的）添加日志记录器
logging.getLogger().addHandler(file_log_handler)
```