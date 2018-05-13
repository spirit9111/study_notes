#sys模块常见函数#

#导入sys模块#
import sys


#sys.argv#
从外部向程序传参数

![](https://i.imgur.com/8Mhg3y2.png)
![](https://i.imgur.com/4qQzDTs.png)

#sys.path#
获取导入模块时搜索的路径
常见用法导入自定义模块
sys.path.append(自定义模块路径)

#sys.exit([arg])#
让程序退出并返回arg的值,arg=0为正常退出

#sys.moudules#
以字典形式返回已导入的模块名

#sys.platform #
获取当前的系统

#sys.version#
获取当前python版本

#相关资料#
http://www.cnblogs.com/wang-yc/p/5623794.html