# Spring

## `注意`

 spring中类如果写了有参构造，则一定要加上无参构造器

## ioc创建对象的三种方式

### 第一种无参构造



### 第二种有参构造

+ 下标赋值

  ```xml
  <bean id="user" class="User">
  	<constructor-arg index="0" value="属性值"/>
  </bean>
  ```

+ 通过类型赋值(如果有两个或以上同属性，则会报错，因此不推荐)

+   ```xml
    <bean id="user" class="User">
    	<constructor-arg type="java.l" value="属性值"/>
    </bean>
    ```

+ 

