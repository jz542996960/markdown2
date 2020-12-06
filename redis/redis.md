###  redis 单线程模型

![image-20201013141436154](assets/image-20201013141436154.png)



![image-20201013141715749](assets/image-20201013141715749.png)

![image-20201013141840277](assets/image-20201013141840277.png)

#### 2  redis 过期策略

![image-20201013143041417](assets/image-20201013143041417.png)

![image-20201013143052812](assets/image-20201013143052812.png)

 redis 对于过期的key 删除策略是 定期删除 + 惰性删除

![image-20201013143534346](assets/image-20201013143534346.png)

![image-20201013143546393](assets/image-20201013143546393.png)

![image-20201013143559574](assets/image-20201013143559574.png)

![image-20201013143749662](assets/image-20201013143749662.png) 

### 手写lru

   linkhashmap   accessOrder = true, 按照访问顺序排序，然后重写removeEldestEntry，判断size 大于 容量



### redis 高可用

   主从同步：

​     步骤 一 全量复制

​       master  node 第一次全量复制，同步bgsvae，生成rdb 快照，把rdb快照文件发给slave，如果生成rdb期间，master接收到了命令，master会把命令写到缓冲区，在slave 保存了RDB后，再把命令复制给slave node。

  步骤二  命令传播

   master node 持续将写命令，异步复制给 slave node，会有延迟问题。

  主从切换过程中会丢失数据



  哨兵模式：

​       哨兵即监控所有的redis服务，哨兵之间也相互监听

​       ![image-20201013150705647](assets/image-20201013150705647.png)

​    故障转移 和leader 选举 

### redis 分布式方案

![image-20201013151020105](assets/image-20201013151020105.png)

​     代理服务：  codis ， codis 需要集群部署，主备切换，key 计算到曹，曹对应的redis



​     服务端实现： 一致性hash算法

### redis 一致性

![image-20201013151929790](assets/image-20201013151929790.png)

   先删除，在跟新：

  ![image-20201013152056624](assets/image-20201013152056624.png)

![image-20201013152106970](assets/image-20201013152106970.png)

  ### 布隆过滤器

​    ![image-20201013153315471](assets/image-20201013153315471.png)

![image-20201013153332614](assets/image-20201013153332614.png)

