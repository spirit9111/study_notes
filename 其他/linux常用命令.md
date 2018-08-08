**ps -ef|grep 进程名**  根据进程名查pid
**sudo netstat -antup**  根据端口查pid

**kill-9** 杀死进程
    
**ls** 				显示当前路径下包含的文件名
**ll**              查看文件包含隐藏文件
**cd** 				进入当前主目录		
mkdir			创建文件夹
mkdir -p a/b/c	创建a文件夹下的b下的c,递归创建
**rm**				删除文件
**cp**				复制
**rmdir**			删除空目录
**pwd** 			显示当前路径
**touch** 文件名x 	创建文件x
**clear**			清空界面内容
**tree**			树结构
**mv**				剪切/重命名
**cat** 		    查看文件内容或者合并内容
**which**		    程序所在文件位置
--help			查看帮助
man				显示使用手册
**>**				输出重新定向,不存在就创建新的,存在就覆盖
**>>**			输出重新定向,在文件末尾追加新内容

more			分屏显示,f下一页/b上一页/q退出/h帮助


|				管道 左端写,右端读

ln -s 源文件	链接文件		软链接(快捷方式,源文件删除则失效,不占空间)
							(不在一个目录时 源文件要 [绝对路径])
ln 源文件	链接文件		硬链接(占空间,不会随着源文件删除而消失)

**find** 				查找文件
**grep** "xxx" yyy.txt			在yyy搜索文本xxx
grep -v						显示不包含xxx的所有行
grep -n						显示所有包含xxx的行
grep -i						忽略大小写


tar		打包
	-c 生成档案文件,创建打包文件
	-v 列出归档解档的详细过程,显示进度
	-f 指定档案文件名称,f后面一定是.tar文件,所以必须放选项最后
	-t 列出档案中包含的文件
	-x 解开档案文件
	-z	:指定压缩包的格式为:file.tar.gz
	-zcvf xxx.tar.gz*
	**-zxvf** xxx.tar.gz
	-jcvf xxx.tar.bz2*.c
	-jxvf xxx.tar.bz2
gzip 压缩
	-d 解压
	-r 压缩所有子目录

zip			压缩
unzip -d	解压

**chmod**		修改权限
**sudo** 		
**sudo -s**		获取超级管理员权限
who
whoami



**apt-get	update**									更新源
**apt-get	install	package**							安装包
**apt-get	remove	package**							删除包
apt-cache	search	package						搜索软件包
apt-cache	show	package						获取包的相关信息,如说明、大小、版本等
apt-get	install	package	--reinstall				重新安装包
apt-get	-f	install								修复安装
**apt-get	remove	package	--purge**					删除包,包括配置文件等
apt-get	build-dep	package						安装相关的编译环境
apt-get	upgrade									更新已安装的包
apt-get	dist-upgrade							升级系统
apt-cache	depends	package						了解使用该包依赖那些包
apt-cache	rdepends	package					查看该包被哪些包依赖
apt-get	source	package							下载该包的源代码
apt-get	clean	&&	sudo	apt-get	autoclean	清理无用的包
apt-get	check									检查是否有损坏的依赖






