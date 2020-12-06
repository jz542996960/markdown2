###   getDeclaredConstructors()  和 getConstructors() 的区别

### 示例

```java
package com.jz.assign;


import java.lang.reflect.Constructor;

class MyDemo{

    private String str;

    private Integer num;
    //私有构造函数
    private MyDemo(String str,Integer num){
        this.str = str;
        this.num = num;
    }

    //共有构造函数
    public MyDemo(String str){
      this.str = str;
    }

    protected  MyDemo(String str,String value){
        this.str = str;
    }
}
public class Consuructor {

    public static void main(String[] args) {

        try {
            Class<?> aClass = Class.forName("com.jz.assign.MyDemo");
            //size 为3 。包含了public 和 private 和 protected 构造方法
            Constructor<?>[] declaredConstructors = aClass.getDeclaredConstructors();
            // size 为1 只有public 构造方法
            Constructor<?>[] constructors = aClass.getConstructors();

            
            Class[] classes = new Class[]{String.class,Integer.class};
            // size 为1 ，有对应入参为string和integer 的方法
            Constructor<?> declaredConstructor = aClass.getDeclaredConstructor(classes);
            //抛出NoSuchMethodException 异常
            Constructor<?> constructor = aClass.getConstructor(classes);

        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }catch (NoSuchMethodException e){
            e.printStackTrace();
        }

    }

}

```



### 总结

<font color=#FF0000 >getDeclaredConstructors()   和 getConstructors() 都会返回类的构造方法，前者会返回 public ，private，protected，default 构造方法，后者只会返回public 构造方法</font>

