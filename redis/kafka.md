batchsize  设置批量发送大小

 Linger.ms 两次间隔时间

消费offset：  earlist  消费最早的消息

 ![image-20201011164557823](assets/image-20201011164557823.png)



## offset  维护在哪里

老的版本维护在zk

新的版本维护在kafka里

/tmp/kafka-logs

![image-20201011165455244](assets/image-20201011165455244.png)

##### 当前的消费者消费到哪里

![image-20201011164752398](assets/image-20201011164752398.png) 



自动提交 间隔时间越长，每个多少秒提交一下，如果取到数据后，消费者挂掉，此时还没有提交，导致消费者重启后，会重复消费

可以关闭自动提交，可通过consumer。commitSync同步提交，也可  consume.commit 异步提交



### 副本机制

副本数是有限制的，不能超过broker 的数量



![image-20201011170428486](assets/image-20201011170428486.png)



每个broker上都有topic 的副本



![image-20201011170449173](assets/image-20201011170449173.png)



#### 副本同步

![image-20201011173503692](assets/image-20201011173503692.png)



isr  优质副本集



### 消息传播

![image-20201011192250284](assets/image-20201011192250284.png)



HW  higth water  表述 数据在所有副本都同步了

LEO  log end offset  

remote leo  远程leo 副本的Leo

![image-20201011213609319](assets/image-20201011213609319.png)

 ack 的值

![image-20201011214013422](assets/image-20201011214013422.png)

# 数据丢失问题

