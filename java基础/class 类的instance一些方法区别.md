##  CLASS类 的一些instance方法的区别



####  Class.isInstance(Object obj)

> 用来判断obj 是否可转化为Class类，不会产生异常，true 可转化 false 不可转化。



```java
package com.jz.assign;


//接口
interface  BaseInterface{

    public void show();

}


//父类A
class BaseA {

}

//父类B
class BaseB {

}

//子类
class A extends BaseA implements BaseInterface{

    @Override
    public void show() {

    }
}

public class ClassTest {

    public static void main(String[] args) {
        A a = new A();
        System.out.println(BaseA.class.isInstance(a));  //true
        System.out.println(BaseB.class.isInstance(a));  //false
        System.out.println(BaseInterface.class.isInstance(a)); //true
    }
}

```







###   public native boolean isAssignableFrom(Class<?> cls)

> 用来判断cla是否是class类的子类，是类相关，不是具体实例相关

 ````java
package com.jz.assign;


//接口
interface  BaseInterface{

    public void show();

}


//父类A
class BaseA {

}

//父类B
class BaseB {

}

//子类
class A extends BaseA implements BaseInterface{

    @Override
    public void show() {

    }
}

public class ClassTest {

    public static void main(String[] args) {
        A a = new A();

        System.out.println(BaseA.class.isAssignableFrom(A.class));  //true
        System.out.println(BaseB.class.isAssignableFrom(A.class));  //false
        System.out.println(BaseInterface.class.isAssignableFrom(A.class)); // true
    }
}

 ````





### instance of 

> 　　instanceof 严格来说是Java中的一个双目运算符，用来测试一个对象是否为一个类的实例，用法为：boolean` `result = obj ``instanceof` `Class

```java
package com.jz.assign;


//接口
interface  BaseInterface{

    public void show();

}


//父类A
class BaseA {

}

//父类B
class BaseB {

}

//子类
class A extends BaseA implements BaseInterface{

    @Override
    public void show() {

    }
}

public class ClassTest {

    public static void main(String[] args) {
        A a = new A();
        System.out.println(a instanceof  BaseA); // true

       // System.out.println(a instanceof  BaseB); //编译不通过
      
        System.out.println(a instanceof  BaseInterface); // true

        System.out.println(a instanceof  Object); // true

        a = null;
        System.out.println(a  instanceof  BaseA); // false
        System.out.println(a  instanceof  Object); // false

        int value = 10;
     //   System.out.println(value instanceof  Integer); //编译不通过，必须为对象类型

        Integer value2 = 10;

        System.out.println(value2 instanceof  Integer); // true

    }
}

```

