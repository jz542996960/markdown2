---
typora-root-url: ./assets
typora-copy-images-to: ./assets
---

### Integer和int的比较
#### 1. 两个new Integer比较
> 通过new生成的Integer变量，实际内存地址不同，所有 == 永远返回false。

```
public class IntegerMain {

    public static void main(String[] args) {
       Integer integer1 = new Integer(100);
       Integer integer2 = new Integer(100);
       System.out.println(integer1 == integer2);
    }
}
返回：false
```
### 2. Integer 和 int 的比较
>Integer变量和int变量比较时，只要两个变量的值是相等的，则结果为true（因为包装类Integer和基本数据类型int比较时，java会自动拆包装为int，然后进行比较，实际上就变为两个int变量的比较）

```
public class IntegerMain {

    public static void main(String[] args) {
       Integer integer1 = new Integer(100);
        int  integer2 = 100;
       System.out.println(integer1 == integer2);
    }
}
返回：true
```
### 3. new Integer 和 Integer 比较
> 非new生成的Integer变量和new Integer()生成的变量比较时，结果为false。（因为非new生成的Integer变量指向的是java常量池中的对象，而new Integer()生成的变量指向堆中新建的对象，两者在内存中的地址不同）

```
public class IntegerMain {

    public static void main(String[] args) {
       Integer integer1 = new Integer(100);
       Integer integer2 = 100;
       System.out.println(integer1 == integer2);
    }
}
返回：false
```
### 4. 两个非new Integer 比较
> 对于两个非new生成的Integer对象，进行比较时，如果两个变量的值在区间-128到127之间，则比较结果为true，如果两个变量的值不在此区间，则比较结果为false

```
public class IntegerMain {

    public static void main(String[] args) {
        Integer a = 100;
        Integer b = 100;
        System.out.print(a==b); //true

        Integer c = 128;
        Integer d  = 128;
        System.out.print(c == d); //false
    }
}

```
----
> Integer a = 100 实际调用的是Integer.valueof方法.

```
   public static Integer valueOf(int i) {
        if (i >= IntegerCache.low && i <= IntegerCache.high)
            return IntegerCache.cache[i + (-IntegerCache.low)];
        return new Integer(i);
    }
    
```
>IntegerCache 是一个static final Integer cache[] 的数组,数据为-128 到127 之间。


