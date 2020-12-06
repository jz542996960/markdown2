



## Spring  factoryBean



```java

@Service
public class FactoryBeanTest implements FactoryBean {
    @Override
    public Object getObject() throws Exception {
        return new MyService();
    }

    @Override
    public Class<?> getObjectType() {
        return MyService.class;
    }

    @Override
    public boolean isSingleton() {
        return true;
    }
}
```





```java
public class MyService {

    public MyService(){
        System.out.println("my service init");
    }

    public void show(){
        System.out.println("1111");
    }
}
```





main方法

```java
 AnnotationConfigApplicationContext annotationConfigApplicationContext = new AnnotationConfigApplicationContext(AppConfig.class);
        MyService myService = (MyService) annotationConfigApplicationContext.getBean(MyService.class);
        MyService myService3 = (MyService) annotationConfigApplicationContext.getBean("factoryBeanTest");
        System.out.println(myService == myService3);
        myService.show();
        myService3.show();
```

输出结果；

```
true
1111
1111
```





源码分析：

```java
@Override
	public <T> T getBean(Class<T> requiredType) throws BeansException {
		assertBeanFactoryActive();
    //调用DefaultListableBeanFactory 的getBean方法
		return getBeanFactory().getBean(requiredType);
	}

```

```java
	@Override
	public <T> T getBean(Class<T> requiredType) throws BeansException {
		return getBean(requiredType, (Object[]) null);
	}

 @Override
	public <T> T getBean(Class<T> requiredType, Object... args) throws BeansException {
		NamedBeanHolder<T> namedBean = resolveNamedBean(requiredType, args);
		if (namedBean != null) {
			return namedBean.getBeanInstance();
		}
		BeanFactory parent = getParentBeanFactory();
		if (parent != null) {
			return parent.getBean(requiredType, args);
		}
		throw new NoSuchBeanDefinitionException(requiredType);
	}	
	
	
```

```
factoryBean  getObject 生成的值放在这里
factoryBeanObjectCache
```