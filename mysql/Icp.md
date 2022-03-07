* 例如 有索引  index(a,b,c)
* 执行 select * from table where a = 1 and b > 0 and c= 1
  * 没有icp,获取满足a = 1 and b > 0的所有数据，就返回。
  * 有icp，获取满足a = 1 and b > 0的所有数据，再根据 c=1 进行过滤，将过滤后的数据返回。 
  * 通过这种方式，可以减少回表的次数
