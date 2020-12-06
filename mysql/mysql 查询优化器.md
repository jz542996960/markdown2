select * from  t1,t2

select * from t1 join t2 是一样的

T2 是驱动表  t1 是被驱动表



![image-20200917195430302](assets/image-20200917195430302.png)



查询优化器：  

·1 准备阶段

2 优化阶段



全表扫描

Innondb space

join buffer   增加join buffer



 ![image-20200917224736196](assets/image-20200917224736196.png)

  

小标驱动大表 

 ![image-20200917231413577](assets/image-20200917231413577.png)

![image-20200917232257836](assets/image-20200917232257836.png)

mysql 会报错

![image-20200917232327824](assets/image-20200917232327824.png)

