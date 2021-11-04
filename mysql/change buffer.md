
http://mysql.taobao.org/monthly/2015/07/01/
* Change buffer的主要目的是将对二级索引的数据操作缓存下来，以此减少二级索引的随机IO，并达到操作合并的效果。
将数据页从磁盘读入内存中涉及随机 IO 访问，这也是数据库里面成本最高的操作之一，而利用写缓存（Change Buffer）可以减少 IO 操作，从而提升数据库性能。 针对非唯一普通索引页有效，因为唯一索引需要校验唯一性。
* 以下几种情况会触发合并操作
 * 从磁盘读入数据到内存
 * 线程定时合并
 * 数据库关闭
 
* 以下几种情况会触发写入磁盘操作
  * 线程定时同步
  * 数据库关闭
  * 缓冲池空间不够
  * redo log写满
* 适合场景
  * 写多读少
  * 唯一索引较少