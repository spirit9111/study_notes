datetime是Python处理日期和时间的标准库
 
## 导入模块 ##
from datetime import datetime

## 获取当前时间 ##
datetime.now()

## 创建指定时间 ##
datetime(2018,5,13,15,30)

## str转换为时间(需要日期和时间的格式化字符串) ##
datetime.strptime('str','格式化')
例:datetime.strptime('2018-5-13 15:42:30','%Y-%m-%d %H:%M:%S')

## 时间转换为str ##
datetime.now().strftime('%a, %b %d %H:%M')

## 相关资料: ##
https://docs.python.org/3/library/datetime.html#strftime-strptime-behavior
