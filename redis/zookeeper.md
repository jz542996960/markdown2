![image-20201010215557940](assets/image-20201010215557940.png)

![image-20201010220326808](assets/image-20201010220326808.png)

zookeeper 分布式协调组件

### 分布式一致性问题





惊群效应



![image-20201010222744127](assets/image-20201010222744127.png)



master 选举 一致性算法

![image-20201010223312371](assets/image-20201010223312371.png)





leader 选举 和数据同步都需要投票

为了提升读的性能，增加了observer，observer不参与投票，只同步数据

![image-20201010223731079](assets/image-20201010223731079.png)

![image-20201010223754481](assets/image-20201010223754481.png)

![image-20201010224407344](assets/image-20201010224407344.png)



![image-20201010230029259](assets/image-20201010230029259.png)



![image-20201010233112426](assets/image-20201010233112426.png)

![image-20201010233125870](assets/image-20201010233125870.png)

![image-20201010234754583](assets/image-20201010234754583.png)

授权 只针对当前会话里授权的



![image-20201011011847541](assets/image-20201011011847541.png)



### node 事件

![image-20201011012237949](assets/image-20201011012237949.png)

### 分布式锁





### zab协议

两阶段提交

![image-20201011094136974](assets/image-20201011094136974.png)

zab解决了  崩溃恢复  和 原子广播

![image-20201011095854509](assets/image-20201011095854509.png)





### 一致性

顺序一致性

