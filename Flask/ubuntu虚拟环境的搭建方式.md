# ubuntu配置虚拟环境 #

----------

配置虚拟环境的**目的**:
将不同项目需要的环境进行隔离,搭建各自需要的运行环境,使得各个项目之间不会相互影响.

虚拟环境**保存的路径**:`home/.virtualenvs/`

需要使用的包及安装命令:
virtualenv:
`sudo pip install virtualenv`

virtualenvwrapper:
`sudo pip install virtualenvwrapper`

**配置环境变量**(不报错则跳过):
1.如果没有`home/.virtualenvs/`文件夹,则需要手动创建.进入home文件夹-->使用命令`mkdir .virtualenvs`创建.
2.在home文件夹中打开(使用gedit/vim都行).bashrc文件添加
```
export WORKON_HOME=$HOME/.virtualenvs
source /usr/local/bin/virtualenvwrapper.sh
```
3.运行命令`source ~/.bashrc`

**创建虚拟环境**(需要联网)
`mkvirtualenv -p python3 虚拟环境名称`

向虚拟环境添加需要的包:
`pip install 包名==版本号`

查看虚拟环境中的已安装的包:
`pip freeze`
`pip list`

虚拟环境的**相关指令**:
查看:
`workon`(回车)

运行:
`workon 虚拟环境名称`

退出:
`deactivate`

删除:
`rmvirtualenv 虚拟环境名称`

**虚拟环境迁移:**
导出包配置(运行相应的环境中)执行,
`pip freeze > 文件名.txt`

导入包配置
`pip install -r 文件名.txt`


报错相关:
locale.Error: unsupported locale setting
`export LC_ALL=C`