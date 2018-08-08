# Celery

### 什么是Celery?
Celery是一种简单/高效/灵活的即插即用的分布式任务队列.

### Celery应用场景?
需要异步处理的任务,发邮件/发短信/上传等耗时的操作.最终到达提升用户体验的目的.

### Celery的模式
Celery主要是由Broker(中间人)和Worker(任务处理者)组成,执行流程为客户端发起任务--->Bocker接收任务,分配给--->Worker处理任务.

### Celery安装
`pip install -U Celery`


### 基本配置:
broker指定消息队列保存的位置
backend指定执行结果保存的位置
```python
from celery import Celery

# 增加配置,redis为例
# 第一种
app = Celery('demo',
             backend='redis://:127.0.0.1:6379/2',
             broker='redis://:127.0.0.1:6379/1')
# 第二种
app = Celery('demo')
app.conf.update(
    broker_url='redis://:127.0.0.1:6379/1',
    result_backend='redis://:127.0.0.1:6379/2',
)
# 第三种,导入.py模块,config中指定broker_url/result_backend
app = Celery('demo')
app.config_from_object('config')
```

### 基本使用

1.配置,创建应用,如上.

2.将异步任务加入到bocker中.
使用装饰器`@app.task`来将任务加入到bocker中.
```python
@app.task
def demo_task():
    print('demo')
    return '任务结果'
```

3.开启worker,处理任务
task为创建应用的.py文件,也就是在app所在模块的统计目录下执行
`celery -A tasks worker --loglevel=info`

4.调用任务
```python
from tasks import demo_task
demo_task.delay() # 如果任务有参数,直接在delay()中传入
```

5.保存结果(非必须)
```python
# ret是一个AsyncResult对象,保存有返回值等信息.
ret = demo_task.delay() 
# 返回值
ret.result
```

### 其他功能
group: 一组任务并行执行，返回一组返回值，并可以按顺序检索返回值。

chain: 任务一个一个执行，一个执行完将执行return结果传递给下一个任务函数.

