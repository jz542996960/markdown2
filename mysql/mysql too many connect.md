### mysql  提示too many connect



```
//重启mysql
service mysqld restart

//链接mysql
 mysql -u root -p
 
 //查看当前设置的最大连接数
 show variables like "max_connections"
 
 //修改最大连接数
 set GLOBAL max_connections=1000
 
```

