![image-20201010170344424](assets/image-20201010170344424.png)

![image-20201010170940203](assets/image-20201010170940203.png)

![image-20201010174617306](assets/image-20201010174617306.png)

![image-20201010175400738](assets/image-20201010175400738.png) 

![image-20201010183356067](assets/image-20201010183356067.png)

set  去重 无序

![image-20201010193807596](assets/image-20201010193807596.png)

随机返回集合

正数 不会重复

负数 会重复

场景： 抽奖 随机事件



![image-20201010194028284](assets/image-20201010194028284.png)

场景：

 1共同好友，推荐游戏



zset

![image-20201010194542962](assets/image-20201010194542962.png)

默认从小到大



![image-20201010194652449](assets/image-20201010194652449.png)

从大到小



OBJECT encoding 可以查看redis  每种数据类型内部存储的类型





zset 内部接口

ziplist，skiplist （最高层 64层）

![image-20201010195920460](assets/image-20201010195920460.png)

![image-20201010200431963](assets/image-20201010200431963.png)

![image-20201010200821806](assets/image-20201010200821806.png)

![image-20201010201217267](assets/image-20201010201217267.png)

aof 重写

开启aof 会断掉 rdb





redis 4.x 以后 可以采用混合模式

![image-20201010201657822](assets/image-20201010201657822.png)

![image-20201010201903651](assets/image-20201010201903651.png)

![image-20201010202248322](assets/image-20201010202248322.png)

redis 默认 是弱一致性



paxos



cp ap  脑裂



![image-20201010203746363](assets/image-20201010203746363.png)



codis  代理算法

![image-20201010210615074](assets/image-20201010210615074.png)