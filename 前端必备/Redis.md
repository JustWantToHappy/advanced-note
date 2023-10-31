## 使用Docker来使用redis
- 使用redis必须使用docker运行redis对应容器,如果要进入到redis-cli客服端，则需要使用docker exec -it 容器id或者容器名称 redis-cli,如果之前还设置了用户密码，则在redis-cli中使用auth 用户密码命令方可进入
- 默认中文会以十六进制的形式展示，如果想要展示中文，可以在使用docker exec命令的使用添加参数--raw
## redis-cli相关命令

- set key value
- setnx key value:设置键值对，如果键已经存在，则不做任何处理，否则新建键值对
- get key
- del key：删除key和对应的value
- exists key:判断key对应的value是否存在
- flushall:删除所有的键值对
- keys *:查看所有的键
- keys *me:查看所有以me结尾的键
- quit：退出redis客服端
- clear ：清空控制台
- ttl key:查看key键过期时间
- expire key 过期时间：给键值对设置过期时间，也可以通过setex key value 过期时间来设置过期时间和值
## 列表

- lpush letter a:表示向数组letter中push一个“a”字符串，注意，每次lpush都是将最新的元素从左到右添加，所以是从头部添加，如果想要从尾部添加，可以使用rpush命令
- lpush letter a b c d e:从左到右依次向数组letterpush多个元素
- lpop和rpop命令：表示分别从列表的头部或者尾部将元素删除
- lpop 数组名称 数字：表示用来删除多个元素
- lrange 数组名称 开始索引 结束索引：获取列表的一个片段
- llen 数组名称：用来查看数组的长度
- ltrim 数组名称 开始索引 结束索引：保留数组中[startIndex,endIndex]中的元素，其他为止的元素都删除
## 集合
Set中的元素是不可以重复的，set命令都是以s开头

- sadd 集合名称 元素：向集合中添加一个元素
- smembers 集合名称：查看集合中所有元素
- sismember 集合名称 元素：查看元素是否在集合中
- srem 集合名称 元素：删除集合中的某个元素
## 有序集合
有序集合的命令都是以z开头,有序集合中的每个值必须关联一个浮点数(分数)，用来进行排序

- zadd 集合名称 数字 值:向集合中添加一个元素，并指定它关联的浮点数
- zrange命令：获取片段，只会输出元素
- zrange 集合名称 开始索引 结束索引 withscores:获取片段，不仅获取到元素，还会获取到对应的分数
- 如果想要查看某个值的分数：zscore 集合名称 值
- zrank 值：查看从小到大的值的排名
- zrevrank 值：查看从大到小的值的排名
## 哈希
哈希都是以h开头的命令

- hset 哈希表名称 key value
- hget 哈希表名称 key
- hgetall 哈希表名称
- hdel 哈希表名称 key
## 发布订阅

- subscribe 频道名称：订阅某个频道
- publish  频道名称 消息内容：指定频道并发布消息
## 消息队列(Stream)
stream的命令都是以x开头

- xadd 消息名称　＊　

