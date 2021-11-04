# Spring整合MyBatis

### 方式一	

使用spring整合MyBatis，就是配置一个spring.xml，

首当其冲需要连接数据库，配置需要配置的bean有SqlSessionFactoryBean（引用数据库源，以及别名、mapper地址，config地址）

，SqlSessionTemplate（引入SqlSessionFactoryBean，他只有构造方法，所以需要配上index=0）

，配置实现类的bean。





#### ———例如———

在resources中spring-dao.xml

```xml-dtd
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:context="http://www.springframework.org/schema/context"
       xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans.xsd http://www.springframework.org/schema/context https://www.springframework.org/schema/context/spring-context.xsd">

    <context:property-placeholder location="classpath*:jdbc.properties"/>
<!--    <context:annotation-config/>-->
<!--    <context:component-scan base-package="com.kuang.mapper"/>-->

    <bean class="com.alibaba.druid.pool.DruidDataSource" id="dataSource">
        <property name="url" value="${jdbc.url}"/>
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

<!--    SqlSessionFactory-->
    <bean class="org.mybatis.spring.SqlSessionFactoryBean" id="sessionFactoryBean">
        <property name="dataSource" ref="dataSource"/>
<!--        绑定Mybatis配置文件-->
<!--        <property name="configLocation" value="classpath:mybatis-config.xml"/>-->
<!--        配置mapper.xml-->
        <property name="mapperLocations" value="classpath:com/kuang/mapper/ActorInfoMapper.xml"/>
        <property name="typeAliasesPackage" value="com.kuang.pojo"/>
    </bean>

<!--    sqlSessionTemplate就是我们之前用的sqlSession-->
    <bean class="org.mybatis.spring.SqlSessionTemplate" id="sqlSession">
<!--        只能使用构造器注入sqlSessionFactory，因为他没有set方法-->
        <constructor-arg ref="sessionFactoryBean" index="0"/>
    </bean>

    <bean id="userMapper" class="com.kuang.mapper.ActorInfoImpl">
        <property name="sqlSession" ref="sqlSession"/>
    </bean>
</beans>
```



当然，需要配置Druid数据库，需要配置resources中的jdbc.properties

```apl
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/cinema?useSSL=false&allowPublicKeyRetrieval=true
jdbc.username=root
jdbc.password=root
```

当然此时还是找不到的，需要添加`<context:property-placeholder location="classpath*:jdbc.properties"/>`才可以搜索到，如果没有重启IDEA。



——com.kuang.pojo.ActorInfo.java

```java
package com.kuang.pojo;

import lombok.Data;
import org.springframework.context.annotation.Bean;

@Data
public class ActorInfo {
    private String actor_id;
    private String name;
    private String name_en;
    private String img;
}
```



——com.kuang.mapper.ActorInfoMapper.java

```java
package com.kuang.mapper;

import com.kuang.pojo.ActorInfo;
import org.springframework.context.annotation.Bean;

import java.util.List;

public interface ActorInfoMapper {
    public List<ActorInfo> selectActorInfo();
}
```



——com.kuang.mapper.ActorInfoImpl.java

```java
package com.kuang.mapper;

import com.kuang.pojo.ActorInfo;
import org.mybatis.spring.SqlSessionTemplate;
import org.springframework.context.annotation.Bean;
import org.springframework.stereotype.Component;

import java.util.List;

public class ActorInfoImpl implements ActorInfoMapper {

    private SqlSessionTemplate sqlSession;

    public void setSqlSession(SqlSessionTemplate sqlSession) {
        this.sqlSession = sqlSession;
    }

    public List<ActorInfo> selectActorInfo() {
        ActorInfoMapper mapper = sqlSession.getMapper(ActorInfoMapper.class);
        return mapper.selectActorInfo();
    }
}
```

实现的时候，需要在spring中进行set注入



### `再次警告！java中的xml文件无法被解析`

```
<build>
    <resources>
        <resource>
            <directory>src/main/java</directory>
            <includes>
                <include>**/*.xml</include>
            </includes>
            <filtering>true</filtering>
        </resource>
        <!--            <resource>-->
        <!--                <directory>src/main/resources</directory>-->
        <!--                <includes>-->
        <!--                    <include>**/*.xml</include>-->
        <!--                </includes>-->
        <!--                <filtering>true</filtering>-->
        <!--            </resource>-->
    </resources>
</build>
```



### 方式二

