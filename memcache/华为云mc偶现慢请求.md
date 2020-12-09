* 华为云mc偶现慢请求,响应时间超过50ms的较多，有的达到1s，和dba确认了下，资源监控未发现异常，所以考虑网络问题。
* 因为配置了多个mc实例，所以想先抓个包看看问题出在哪里。
* 步骤
  
  1、 对某个容器抓包，同时观察日志，当慢查询日志出现时，停止抓包，将抓包数据拉到本地。
  
  2、 wireshark打开，memcache.key eq $log.memcaceh.key
  
   ![image](https://github.com/qiuyuexi/book/blob/master/mc%E6%8A%93%E5%8C%851.png)
 
  3、 右键follow, 点击tcp stream 
  
   ![image](https://github.com/qiuyuexi/book/blob/master/mc%E6%8A%93%E5%8C%852.png)
  
  4、 发现问题，建连超时，tcp重传。
  
  5、 反馈问题
