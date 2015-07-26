#### 1.mysql中文乱码问题
* 对于mysql5.5版本，需要在`/etc/mysql/my.cnf`做如下修改：
[client]下添加：`default-character-set = utf8`
[mysqld]下添加：`character-set-server = utf8`  
   
* 对于mysql5.5之前的版本，做如下修改：
在[client] 和 [mysqld]下都添加一行
`default-character-set = utf8`
**如果在mysql5.5 版本中也这么配置会导致mysql服务起不来。**