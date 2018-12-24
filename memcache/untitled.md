---
description: key过期排查
---

# Untitled

php设置key-value,过期时间300s。

设置成功后立即获取，发现返回false，key过期了。

将过期时间设置为30000s后,读取正常。

1. 首先怀疑是否内存满了，并且key 对应的slab也没有多余空间，用memcached-tool 测试了一下，发现内存还很充足,也没有触发Lru，只能从其他方面排查。 

2. telnet 127.0.0.1 11211 使用命令模拟Php的写入读取，发现是正常的 。

3.  定位k-v写入的时候归属于哪个slab,编号x 

telnet 127.0.0.1 11211

stats cachedump x 10 

显示  

ITEM key \[count b; expire\_time s\] 

拿出过期时间计算,发现过期时间是期望时间，那么设置是没有问题的。 

使用get key ,发现key 居然过期了。

由于mc是在get的时候才判断key是否过期，

那么在当前时间，被认为过期了。

在mc实例所在服务器执行date,发现服务器时间异常。

重设服务器时区，恢复正常。

