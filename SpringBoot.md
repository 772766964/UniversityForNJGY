# SpringBoot

springboot最核心的就是**自动装配**

## 流程

java:OOP

mysql:持久层

html+css+jquery+框架：视图，框架不熟练，css不好；

javaweb：独立开发MVC三层架构的网站：原始

ssm：框架：简化了我们的开发流程，配置也开始较为复杂

**war：tomcat运行**

spring再简化：SpringBoot- jar：内嵌tomcat；微服务架构

服务越来越多：springcloud；

## 什么是Spring

Spring是为了解决企业级应用开发的复杂性而创建的，简化开发

## Spring是如何简化Java开发的

简单来说是通过IOC、AOP，一个个Bean，通过切面、模板减少样式代码

## 一个简单的api实例

将application.properties 重命名为 application.yml，并添加内容（要有idea提示，不然运行不了）

`2021年12月1日 ， 必须要有提示也许是因为我们在：后面没有加空格。。。`

``` yaml
server:
  port: 8888
spring:
  datasource:
    driver-class-name: com.mysql.jdbc.Driver
    url: jdbc:mysql://127.0.0.1:3306/ssm_db?useSSL=false&allowPublicKeyRetrieval=true
    username: root
    password: root

mybatis:
  mapper-locations: classpath:mapper/*.xml
```

配置完就可以简单的运行查看error页面了。

创建数据库的实体模型entity的User.java

``` java
package com.example.demo.entity;
import org.springframework.context.annotation.Bean;

@Data
@AllArgsConstructor
@NoArgsConstructor
@Setter
@Getter
public class User {
    private String uuid;
    private String userName;
    private String password;
    private String realName;
    private String gender;
    private String birthday;
}
```

在路径下创建mapper，UserMapper.java文件

``` 	java
package com.example.demo.mapper;

import com.example.demo.entity.User;
import org.apache.ibatis.annotations.Mapper;
import java.util.List;

@Mapper
public interface UserMapper {
    public List<User> findAll();
}
```

在resource中创建UserMapper.xml文件

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.example.demo.mapper.UserMapper">
    <select id="findAll" resultType="com.example.demo.entity.User">
        SELECT * FROM `user`
    </select>
</mapper>
```

——UserService.java

```java
package com.example.demo.service;

import com.example.demo.entity.User;
import com.example.demo.mapper.UserMapper;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.util.List;

@Service
public class UserService {
    @Autowired
    private UserMapper userMapper;
    public List<User> findAll(){
        return userMapper.findAll();
    }
}
```

在路径下创建controller的UserController.java文件

``` java
package com.example.demo.controller;

import com.example.demo.entity.User;
import com.example.demo.service.UserService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import java.util.List;

@RestController
public class UserController {

    @Autowired
    private UserService userService;

    @RequestMapping("/abc")
    public User getName(){
        return new User("a","b");
    }
    @RequestMapping("/abcd")
    public List<User> getUser(){
        return userService.findAll();
    }
}
```

## 一个简单的项目

``` java
package com.example.demo;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
@RestController
public class DemoApplication {

public static void main(String[] args) {
	SpringApplication.run(DemoApplication.class, args);
}

@GetMapping("/hello")
public String hello(@RequestParam(value = "name", defaultValue = "World") String name) {
	return String.format("Hello %s!", name);
}
}
```

这里我们用到了

+ @GetMapping ("/*") 配置路径，http://localhost:8080/hello
+ @RequestParam(Value="",defaultValue="") 赋值以及默认赋值

**windows使用**

``` 
mvnw spring-boot:run
```

**MacOS/Linux:**

```
./mvnw spring-boot:run
```

What should happen if you add `?name=Amy` to the end of the URL?

## yaml 的使用

—yaml写法—

``` yaml
# 普通的key - value
name: xl

# 对象
students:
	name: xl
	age: 22

# 对象·行内写法
students: {name: xl, age: 3}

# 数组
pets:
	- cat
	- dog
	- pig

# 数组·行内写法
pets: [cat,dog,pig]
```

—propertities写法—

``` properties
name=xl

student.name=xl
student.age=2
```

### `Yaml`  和   `Properties` 的区别在哪呢？

properties 只能保存键值对！

**yaml 除了保存键值对还可以保存数组，对象**

也就是说yaml可以给我们的实体类赋值

|  | yaml | properties |
| :-----| :---: | :----: |
| 功能 | 批量注入配置文件中的属性 | 一个个指定   *@Value("name")* |
| 松散绑定（松散语法） | 支持 | 不支持 |
| SpEL | 不支持 | 支持 |
| JSR303数据校验 | 支持 | 不支持 |
| 复杂类型封装 | 支持 | 不支持 |

**松散绑定**  		firstName 能绑定 first-name

**JSR303校验** 	在类上标注@Validated 数据校验 

​						 之后在字段上标注万能的 @Pattern 正则表达式

​						 更多功能见 JSR-303.md



 

#### *区别总结*

​	如果某个业务只需要一个或部分值，可以使用properties

​	其他情况或者需要编写JavaBean和配置文件进行映射的时候，推荐使用yaml

### @PropertySource（扩展）

写法:@PropertySource(value="classpath:xl.properties")

——xl.properties

``` properties
name=xl
```

——Student.java

``` java
@Component
@PropertySource(value="classpath:xl.properties")
class Student{
    // properties 需要通过SPEL 表达式取出配置文件的值
    @value("${name}")
    String name;
    int age;
}
```

#### 乱码？

在 settings 中搜索  properties  -->  选择  UTF-8 , 再勾选 Ascii

### @ConfigurationProperties（常）

`使用该注解会提示爆红，不解决也可以运行`

解决也很简单，指定实体类，@ConfigurationProperties(prefix="person")

这个时候再假设有一个Student类

``` java
@Component
@ComfigurationProperties(prefix="person")
class Student{
    String name;
    int age;
}
```

#### spring的el表达式

``` yaml
student:
	name: xl${random.uuid}
	age: ${random.int}
	#如果有hello就取值，反之取值hello
	alise: ${student.hello:hello}
```

## @SpringBootTest

### @Test

类似Junit 测试

## 多环境配置及配置文件位置

`file:./config/`

`file:./`

`classpath:/config`

`classpath:./`

classpath 类路径（resource文件），如果同时有这四个，将优先配置上面的



## Spring Boot Web开发

