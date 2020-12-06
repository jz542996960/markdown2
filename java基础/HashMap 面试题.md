## HashMap 面试题

####    1.  HashMap 是如何计算确定key在数组的哪个下标的？

   1.  计算key的hash值

      ```java
        static final int hash(Object key) {
              int h;
              return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
          }
      ```

      ​      我们会发现，它并不是 key 本身的 hashCode，而是来自于 HashMap 内部的另外一个 hash 方法。注意，为什么这里需要将高位数据移位到低位进行异或运算呢？这是因为有些数据计算出的哈希值差异主要在高位，而 HashMap 里的哈希寻址是忽略容量以上的高位的，那么这种处理就可以有效避免类似情况下的哈希碰撞。

2.  通过计算的hash值 确定下标

   ```java
   if ((p = tab[i = (n - 1) & hash]) == null)
               tab[i] = newNode(hash, key, value, null);
   ```

    通过步骤1 计算出的hash值 与数组长度减一进行与运算，计算出具体要存放的数据下标。 其实就是hash值 除以 数组长度，取余数。但是在数组只有在数据长度为 2的幂次方时候 hash % length  ==  (length - 1) & hash。

   

   ### 2. 为什么HashMap的数组长度必须为2的整数幂

   ​      HashMap的长度为10，则Length - 1为9，也就是二进制的1001，通过Hash算法得到的最终index为8，当只有一个元素的时候这没问题。但是我们再来试一个hashCode：100 1000 0101 0101 1110 1110时，通过Hash算法得到的最终的index也是8，另外还有100 1000 0101 0101 1110 1000得到的index也是8。也就是说，即使我们把倒数第二、三位的0、1变换，得到的index仍旧是8，说明有些index结果出现的几率变大！！而有些index结果永远不会出现，比如二进制0000.

   这样，显然不符合Hash算法均匀分布的要求。

   反观，长度16或其他2的幂次方，Length - 1的值的二进制所有的位均为1，这种情况下，Index的结果等于hashCode的最后几位。只要输入的hashCode本身符合均匀分布，Hash算法的结果就是均匀的。

   

   

   ### 3. 为什么不直接使用红黑树，而是在链表长度超过8且数组长度大于64才 转化为红黑树

   https://blog.csdn.net/sinat_41832255/article/details/88884586?utm_medium=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.edu_weight&depth_1-utm_source=distribute.pc_relevant.none-task-blog-BlogCommendFromMachineLearnPai2-3.edu_weight

   

   

   

   

   

   

   

   

   

   

   