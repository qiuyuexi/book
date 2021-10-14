# Curl 使用注意项总结



### CURLOPT\_CONNECTTIMEOUT\_MS

* 使用curl 时，需要设置链接超时时间， 以毫秒为单位。

```text
CURLOPT_CONNECTTIMEOUT_MS = xxms
```

* 设置超时时间后，发现curl 错误信息都是time out 。看了下手册发现，需要额外设置一个东西

```text
///libcurl使用的是标准名称的解析器，内部传输信息号部分，依然是使用秒来计算是否超时，并且最少时间是1秒，如果想要设置超时时间小于1秒，那么直接通过CURLOPT_NOSIGNAL禁用信号即可
CURLOPT_NOSIGNAL => 1
CURLOPT_CONNECTTIMEOUT_MS = xxms
```



