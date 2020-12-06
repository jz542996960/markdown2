### Java异常处理

---

#### 	一 :  Java标准异常

> Throwable 这个java类被用来表示任何可以作为异常被抛出的类。Throwable对象可分为两种类型(指从Throwable继承而得到的类)：Error用来表示编译时和系统错误；Exception是可以被抛出的基本类型，通常程序员需要关心的更多是Exception



### 二： RunTimeException

> 运行时异常的类型有很多，他们会自动被java虚拟机抛出，所以不必在异常说明中把他列出来。这些异常都是从RunTimeException中继承而来。RunTimeException也被称为 **不受检查异常**



### 三： RunTimeException和Exception的区别

1. ```java
   package com.jz.test.finallyTest;
   
   public class CheckException {
   
       public static void outException() throws InterruptedException {
           Thread.currentThread().sleep(1000);
       }
   
   
       public static void main(String[] args) {
           try {
               outException();
           } catch (InterruptedException e) {
               e.printStackTrace();
           }
       }
   }
   
   ```



> 代码中抛出的InterruptedException继承自Exception，为受检异常。必须在代码里catch，转化为非受检异常。或者在方法外边throws Exception。然后调用改方法的方法必须要catch到该异常或者继续往上层抛出异常。

  ```
package com.jz.test.finallyTest;

public class UnCheckException {

    public static void getUnCheckException(){

       throw new BusinessException("1112","1213");
    }

    public static void main(String[] args) {

        try{
            getUnCheckException();
        }catch (BusinessException e){
            System.out.println("Code:" + e.getCode() + " msg" + e.getMsg());
        }
    }
}

  ```

> 上边的代码中抛出的是非受检异常，所有不用再方法外边throws抛出的异常。调用方法的方法也不是必须catch到该异常。

```
package com.jz.test.finallyTest;

public class UnCheckException {

    public static void getUnCheckException(){

       throw new BusinessException("1112","1213");
    }

    public static void main(String[] args) {

       getUnCheckException();
    }
}

```

> 从上边的代码可以看到，非受检异常，调用方不必必须catch到该异常。如果RunTimeException没有被捕获而直达main方法，那么在程序退出之前将调用异常的printStackTrace()方法。

### 四： finally 返回值

> 当要把出内存之外的资源恢复到它们的初始状态，就要用到finally字句。需要清理的资源包括已经打开的文件或者网络连接等，只要进入到try 语句块，finaly总是会执行。但是在finally中如果有返回值，程序该如何执行呢

-----

finally不修改返回值，直接返回基础数据类型：

```
package com.jz.test.finallyTest;

public class FinallyTest {

    public static int add(int a,int b ){

        try{
            return a+b;
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            return a-b;
        }
    }


    public static int getValue(){

        int a =100;
        try{
            return a;
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            return 300;
        }

    }

    public static void main(String[] args) {
        System.out.println(add(10,11));
        System.out.println(getValue());

    }
}
打印结果：
-1
300
```

> 从打印的结果可以看出，如果finally中有返回值，那么整个程序的return就会从finally语句中的代码块返回。



### 五： finally不return，修改返回值

##### 5.1 finally修改基本数据类型：

```
package com.jz.test.finallyTest;

public class FinallyRetTest {

    private static int a = 3;

    public static int finallyRet(){
        try{
           return a;
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            a = 10;
        }

        return a;
    }

    public static void main(String[] args) {

        System.out.println(finallyRet());
    }

}
返回：3
```

-----

##### 5.2 finally修改引用类型:

```

package com.jz.test.finallyTest;


class People{

    private String name;
    private String age;

    public People(String name,String age){
        this.age = age;
        this.name = name;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getAge() {
        return age;
    }

    public void setAge(String age) {
        this.age = age;
    }

    @Override
    public String toString() {
        return "Age:" +age + " name:" + name;
    }
}


public class FinallyObjTest {

    public static People getPeople(){

        People people = new People("张三","1213");

        try{
            people.setAge("20");
            people.setName("李四");

            return people;
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            people.setAge("30");
            people.setName("王五");
        }

        return people;

    }

    public static void main(String[] args) {
        System.out.println(getPeople());
    }
    //Age:30 name:王五
}

```

##### 5.3 finally修改基本数据类型包装类

```
package com.jz.test.finallyTest;

public class FinallyRetTest {

    private static Integer a = 1;

    public static int finallyRet(){
        try{
           return a;
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            a = 10;
        }

        return a;
    }

    public static void main(String[] args) {

        System.out.println(finallyRet());
    }

}
返回：1
```

```
package com.jz.test.finallyTest;

public class FinallyRetTest {

    private static Integer a = new Integer(128);

    public static int finallyRet(){
        try{
           return a;
        }catch (Exception e){
            e.printStackTrace();
        }finally {
            a = 129;
        }

        return a;
    }

    public static void main(String[] args) {

        System.out.println(finallyRet());
        System.out.println("a的值为:"+ a);

    }

}
返回： 128
a的值为129
```

>  从结果可以看出finally中修改返回值，如果返回值是基本数据类型包括基本数据类型的包装类，则返回值不会受finally中修改的影响。如果是引用类型，则会收到finally中修改值的影响。