# emoji 查询



* t 字段存储字符串，含有emoji表情，并且做唯一索引。
* 写入一条数据 t字段内容为: 1234emoji1
* 这时候查询 select \* from table where t = 1234emoji2

  结果返回的是emoji1这条数据。

* 经过测试，部分emoji表情会有这种情况

  因为emoji可能会超过4个字节。设置该列 SET utf8mb4 COLLATE utf8mb4\_unicode\_520\_ci解决

  **全角半角**

  以下俩种方式都会区分

* utf8mb4\_general\_ci: 对emoji支持不全
* utf8mb4\_bin: 区分大小写

