## JDK7 下 HashMap 多线程死锁分析

   jdk7下在多线程扩容时候，会引发死锁。

  

   ### 单线程场景

​     扩容前：

​    ![image-20200906085837182](assets\image-20200906085837182.png)

  

  触发扩容后：

​     ![image-20200906085903521](assets\image-20200906085903521.png)

jdk7 下的扩容是基于头插法，扩容后会存在倒叙情况。 单线程场景下扩容没有问题。



## 并发场景下的扩容机制



扩容的代码（transfer）

```java
 void transfer(Entry[] newTable, boolean rehash) {
        int newCapacity = newTable.length;
        for (Entry<K,V> e : table) {
            while(null != e) {
                //1
                Entry<K,V> next = e.next;
                if (rehash) {
                    e.hash = null == e.key ? 0 : hash(e.key);
                }
                int i = indexFor(e.hash, newCapacity);
                e.next = newTable[i];
                newTable[i] = e;
                e = next;
            }
        }
    }
```



​    原始HashMap 扩容前结构 

​    ![image-20200906090114453](assets\image-20200906090114453.png)

​    

  假设trd1 执行完   Entry<K,V> next = e.next 后，线程二 开始执行 。 线程二执行结束后HashMap 变为 链表的结构变为（7，value)->(5,value)->(3,value)

![image-20200906112539420](assets\image-20200906112539420.png)

​    

​      

线程一开始执行第一次循环（e == (3,value), next = (5.value)）

![image-20200906112831035](assets\image-20200906112831035.png)

线程一 第二次循环 （e = (5,value),next = (3,value))，循环接收后变为



![image-20200906113224732](assets\image-20200906113224732.png)

线程一 第三次循环，（e = (3,value),next = (null)）,循环结束后变为

   ![image-20200906113414973](assets\image-20200906113414973.png)



可以看到（3，value）->(5,value),(5,value)->(3,value)。 循环链表出现。 如果有一个get 或者put 方法要放到index为2 位置就会出现死循环。



