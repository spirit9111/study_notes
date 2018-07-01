# ubuntu下redis安装配置 #

----------

**安装**
1.下载:`wget http://download.redis.io/releases/redis-4.0.9.tar.gz`
2.解压:`tar xzf redis-4.0.9.tar.gz`
3.移动文件:`sudo mv ./redis-4.0.9 /usr/local/redis/`
4.进入到redis文件夹:`cd /usr/local/redis/`
5.生成redis:`sudo make`
6.测试redis:`sudo make test`
7.安装redis到/usr/local/bin/文件下:`sudo make install`

使用以上命令后,已经可以使用redis了,运行将使用默认的redis配置文件.
如果需要按照指定配置运行redis,则需要额外进行以下步骤:

8.一般情况下是,将默认的redis配置文件redis.conf(路径为:/usr/local/redis/redis.conf), 复制到etc/redis文件夹(redis需要手动创建)下
命令操作在/etc下执行`mkdir redis`,
然后`sudo cp /usr/local/redis/redis.conf /etc/redis/`
9.修改redis.conf后,运行`sudo redis-server /etc/redis/redis.conf `

**配置**

| 常用参数 | 介绍 |
| --- | --- |
|   bind 127.0.0.1 | 指定server运行的ip,默认127.0.0.1 |
|  port 6379 | 指定运行的端口,,默认6379 |
| **daemonize** no | 是否开启守护进程,开启(yes)后redis服务器会在后台运行,而不会阻塞命令行 |
| dbfilename dump.rdb | 指定本地数据库文件名 |
|  dir ./ | 指定本地数据库存放目录 |
| logfile  | 日志文件存放地址 |
| slaveof | 主从配置相关 |

