---
description: '最近在看tcp/ip，看到ip地址基础知识相关部分,发现忘得差不多了，特意查了些资料。复习了下'
---

# 子网划分

![&#x56FE;&#x7247;&#x6765;&#x81EA;&#x7F51;&#x7EDC;](../.gitbook/assets/qi-ye-wei-xin-jie-tu-6623e1cb248249e5b0445cf5791f886b.png)

 子网划分，需从主机部分借几位，与网络部分构成子网网络部分。 

根据"与"特性,1 & 1 = 1; 1 & 0 = 0; 

ip地址 网络地址 + 主机地址。

 掩码全部1的位置标识网络部分。

 因此 ip 地址 & 掩码 可得出网络部分。

 ip地址 与 掩码非1部分取反与得出主机部部分

