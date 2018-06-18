# git常用命令 #

----------

设置用户名,邮箱
`git config --global user.name "Your Name"`
`git config --global user.email "email@example.com"`

初始化,自动添加.git文件
`git init`

添加
`git add <file>`

提交
`git commit -m <message>`

推送到github
`git push origin master`

克隆远程库
`git clone ssh_addr`

查看当前状态
`git status`

查看变更的内容
`git diff`

查看提交的历史记录
`git log`

查看命令日志,可以查找到每一次操作对应的id
`git reflog`

撤销对文件的改动(本质是版本库替换工作区)
`git checkout -- file`

还原版本,num为上几次操作
`git reset --hard HEAD^num`(回到过去)
或者是`git reset --hard ID`(返回未来)

从版本库删除
`git rm file`然后commit

设置标签
`git tag -a 标签名 -m '标签描述'`

推送标签
`git push origin 标签名`


删除本地标签
`git tag -d 标签名`

删除远程仓库标签
`git push origin --delete tag 标签名`


查看当前分支
`git branch`

切换分支
`git checkout -b dev`

推送分支
`git push -u origin 分支`

合并分支
`git merge 分支`



## 连接github步骤 ##

1.`ssh-keygen -t rsa -C "youremail@example.com"`
2.找到.ssh文件夹下的id_rsa.pub,复制内容
3.登录github,添加密钥
