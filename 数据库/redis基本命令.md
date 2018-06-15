# Redis基本命令 #

----------

## 基本命令: ##

开启redis服务器:`sudo redis-server`
开启redis客户端:`redis-cli`
切换数据库:`select db_num`
PINB:`ping`
清空当前数据库:`flushadb`
清空全部数据库:`flushall`
数据操作-**增删改查**

键命令:

| 键命令 | 形式 | 介绍 |
| --- | --- | --- |
| **keys** | keys pattern | 查询键,支持正则  |
| **del** | del key1 key2 ... | 删除键 |
| **exists** | exists key1 key2 ... | 判断键是否存在,返回存在的个数 |
| type | type key | 判断键对应值的类型 |
| expire | expire key seconds | 设置超时时间 |
| ttl | ttl key | 查看有效时间 |

**string**
字符串
----------

增/改:
```
# 单个数据添加
set key value
# 多个数据添加
mset key1 value1 key2 value2 ...
# 追加数据,在原有的value基础上追加
append key value
# 添加超时时间,超时自动销毁数据
setex key seconds value
set key value ex seconds
```
查:
```
# 单个查询
get key
# 多个查询
mget key1 key2 ...
```

删:
`del key1 key2 ...`

**hash**
一般用于保存对象-对象属性-属性值
----------

增/改:
```
# 单个数据添加
hset key field value
# 多个数据添加
mset key1 value1 key2 value2 ...
```
查:
```
# 查询key对应的所有field
hkeys key
# 查询key下所有的值
hvals key
# 获取指定key下field的值
hget key field
# 获取多个key下的field的值
hmget key field1 field2 ...
```
删:
`hdel key field1 field2 ...`

**list**
列表
----------
增/改:
```
# 从左添加
lpush key value1 value2 ...
# 从右添加
rpush key value1 value2 ...
# 指定位置插入
linsert key before或after 现有元素 新元素
# 修改指定索引的值
lset key index value
```
查:
```
# 查询索引范围内的值,start=stop时查询指定位置的值,0 -1表示查询全部
lrange key start stop

```
删:
```
# 根据value删除k-w
# 如果有重复内容 count 0 表示移除全部,>0从左往右删指定个数,<0从右往左删除指定个数 
lrem key count value
```

set
无序集合
----------
增/改:`sadd key member1 member2 ...`
查:`smembers key`
删:`srem key`

zset
有序集合,可以按照score(权重)排序
----------
增/改:`zadd key score1 member1 score2 member2 ...`
查:
```
# 查询指定范围的value
zrange key start stop
# 按权重查询value
zrangebyscore key min max

```
删:
```
# 删除
zrem key member1 member2 ...
# 按照权重删除
zremrangebyscore key min max
```
