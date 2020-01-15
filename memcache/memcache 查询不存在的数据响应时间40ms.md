* memcache 查询不存在的数据响应时间为40ms 怀疑是网络问题，用tcpdump抓了个包，在wireshark上看了下，突然发现问题
* 客户端使用二进制协议时，mc使用get_key quietly_request 查询数据，如果没有数据 则不返回(40ms后，服务端返回ack)
* 客户端发送 no-op request 来检测是否有查询到数据
* 服务端返回 no-op response 确认没有查询到数据
* 所以，在客户端实例化时，设置Memcached::OPT_TCP_NODELAY= true
![image](https://github.com/qiuyuexi/book/blob/master/memcache/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_f03b6680-ac02-41c1-bda9-ba58a5caaa72.png)
![image](https://github.com/qiuyuexi/book/blob/master/memcache/%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_f6c517d7-ccd6-45aa-acac-8658458d38b3.png)
