# 1Redis的学习使用

## 1.1介绍

REmote DIctionary Server(Redis) 是一个由Salvatore Sanfilippo写的key-value存储系统。

Redis是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存亦可持久化的日志型、Key-Value数据库，并提供多种语言的API。

它通常被称为数据结构服务器，因为值（value）可以是 字符串(String), 哈希(Hash), 列表(list), 集合(sets) 和 有序集合(sorted sets)等类型。

## 1.2命令

redis-cli -h host -p port -a password

redis-cli -h 主机IP地址 -p 端口号 -a 密码

链接完成之后输入ping  返回pong则为链接成功

有时候会有中文乱码。

要在 redis-cli 后面加上 --raw

## 1.3Redis keys命令

del key 该命令用于key存在时删除key

exists key 检查给定key是否存在

expire key seconds 为给定key设置过期时间 以秒计，过时之后将删除这个key

expireat key timestamp EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。

pexpire key milliseconds 设置key的过期时间以毫秒计

keys pattern 查找所有符合给定模式的key

move key db 将当前数据库的key移动到给定的数据库db当中

persist key 移除key的过期时间，key将持久保持

rename key newkey 修改key的名称

type key 返回key所储存的值的类型

## 1.4redis字符串

set key value 设置指定key的值

get key 获取指定key的值

getrange key start end 返回key中字符串值的子字符

getset key value 将给定 key的值设为value，并返回key的旧值（old value）

mget key1 [key2...] 获取所有（一个或多个）给定key的值

setex key seconds value 将值value关联到key，并将key的过期时间设置为seconds（以秒为单位）

setnx key value 只有在key不存在时设置key的值

strlen key 返回key所储存的字符串值的长度

mset key value [key value...] 同时设置一个或多个key-value对

msetnx key value [key value...] 同时设置一个或多个key-value对，当且仅当所有给定key都不存在

incr key 将key中储存的数字值增加一（可以直接使用，直接从null变为1）

incrby key increment 将key所储存的值加上给定的增量值（increment）

incrbyfloat key increment 将key所储存的值加上给定的浮点增量值（increment）

decr key 将key中储存的数字值减一

decrby key decrement  key所储存的值减去给定的减量值（decrement）

append key value

如果key已经存在并且是一个字符串，append命令将制定的value追加到该key原来值（value）的末尾

## 1.5redis 哈希（hash）

hdel key field1 [field2] 删除一个或多个哈希表字段

hexists key field 查看哈希表key中，指定的字段是否存在

hget key field 获取存储在哈希表中指定字段的值

hgetall key 获取在哈希表中指定key的所有字段和值

hincrby key field increment 为哈希表key中的指定字段的整数值加上增量increment

hincrbyfloat key field increment 为哈希表key中的指定字段的浮点数值机上增量increment

hkeys key 获取所有哈希表中的字段

hlen key 获取哈希表中字段的数量

hmget key field1 [field2...] 获取所有给定字段的值

hmset key field1 value1 [field2 value2...] 同时将多个field-value（域-值）对设置到哈希表key中

hset key field value 将哈希表key中的字段field的值设置为value

hsetnx key field value 只有在字段field不存在时，设置哈希表字段的值

hvals key 获取哈希表中所有值

## 1.6redis列表（list）

blpop key1 [key2...] timeout 移出并获取列表的第一个元素，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止

brpop key1 [key2] timeout 移出并获取列表的最后一个元素，如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止

brpoplpush source destination timeout 从列表中弹出一个值，将弹出的元素插入到另外一个列表中并返回它；如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。

lindex key index 通过索引获取列表中的元素

linsert key before|after pivot value 在列表的元素前或后插入元素

llen key 获取列表长度

lpop key 移出并获取列表的第一个元素

lpush key value1 [value2...] 将一个或多个值插入到列表头部

lpusx key value 将一个值插入到已存在的列表头部

lrange key start stop 获取列表指定范围的元素

lrem key count value 移出列表元素

lset key index value通过索引设置列表元素的值

ltrim key start stop 对一个列表进行修剪（trim），就是说，让列表只保留指定区间的元素，不在指定区间之内的元素都将被删除。

rpop key 移出列表的最后一个元素，返回值为移除的元素

rpoplpush source destination 移除列表的最后一个元素，并将该元素添加到另一个列表并返回

rpush key value1 [value2...] 在列表中添加一个或多个值

rpushx key value 为已存在的列表添加值

## 1.7redis集合（set）

sadd key member1 [member2...] 向集合添加一个或多个成员

scard key 获取集合的成员数

sdiff key1 [key2...] 返回第一个集合与其他集合之间的差异

sdiffstore destination key1 [key2...]返回给定所有集合的差集并存储在destination中

sinter key1 [key2...] 返回给定所有集合的交集

sinterstore destination key1 [key2...] 返回给定所有集合的交集并存储在destination中

sismember key member 判断member元素是否是集合key的成员

smembers key 返回所有成员

smove source destination member 将member元素从source集合移动到destination集合

spop key 移出并返回集合中的一个随机元素

srandmember key [count] 返回集合中一个或多个随机数

srem key member1 [member2] 移除集合中一个或多个成员

sunion key1 [key2] 返回所有给定集合的并集

sunionstore destination key1 [key2] 所有给定集合的并集存储在destination集合中

## 1.8redis 数据备份和恢复

save 用于创建当前数据库的备份，此命令将在安装目录中创建dump.rdb文件

如果需要恢复数据，只需要将备份文件（dump.rdb）移动到redis安装目录并启动服务即可。

获取redis目录可以使用config命令，config get dir 获取redis安装目录

bgsave 创建redis备份文件也可以使用命令bgsave，该命令在后台执行

## 1.9redis安全

可以通过config get requirepass这个命令查看是否设置了密码验证，如果密码为空串，意味着无需密码验证就可以连接到redis服务。

config set requirepass “123456” 设置密码为123456

auth password 验证密码

