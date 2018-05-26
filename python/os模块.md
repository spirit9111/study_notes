# os模块常见方法 #

## 导入os模块 ##
import os

## os.getcwd() ##
获取当前所在路径,相当于linux的pwd命令

## os.listdir(path) ##
以list的形式获取指定路径下的文件名,无参数则为当前路径


## os.remove(path) ##
删除指定文件

## rmdir(path) ##
删除文件夹

## os.mkdir(path) ##
创建文件夹(一层)

## os.makedir(path) ##
递归创建文件夹(多层)

## os.path.exists(path) ##
判断指定文件是否存在,返回True/False

## os.name() ##
判断当前的系统平台，Windows返回'nt';Linux返回'posix'

## os.system ##
执行shell命令

## 相关资料 ##
http://www.runoob.com/python3/python3-os-file-methods.html