# MyBatis

`为什么使用`

方便

简化（传统JDBC代码复杂）

框架

自动化

易上手

持久层，原名iBatis,从Apache software foundation迁移到googole code。

`持久层`

+ 将程序的数据在持久状态和顺势状态转化的过程

+ 内存：断电即失

+ 数据库（jdbc），io文件持久化

+ 生活：冷藏，罐头。

`为什么需要持久化`

  Dao层、Service层,Controller层

## 一个程序

`思路：搭建环境-->导入Mybatis-->编写代码-->测试`

总结：需要先创建一个核心xml，然后创建实体类（在核心起个别名），根据实体类创建dao/mapper（接口），实现的时候使用xml，最后注册到核心mybatis-config.xml中(如果最后无法编译java下的xml文件则需要加入以下代码)

——pom.xml

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



——mybatis-config.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<configuration>

    <typeAliases>
        <package name="com.kuang.pojo"/>
    </typeAliases>

    <environments default="development">
        <environment id="development">
            <transactionManager type="JDBC" />
            <!-- 配置数据库连接信息 -->
            <dataSource type="POOLED">
                <property name="driver" value="com.mysql.jdbc.Driver" />
                <!--                ?autoReconnect=true&amp;useSSL=true&amp;characterEncoding=UTF-8&amp;useUnicode=true-->
                <property name="url" value="jdbc:mysql://localhost:3306/cinema?autoReconnect=true&amp;useSSL=false" />
                <property name="username" value="root" />
                <property name="password" value="root" />
            </dataSource>
        </environment>
    </environments>


    <mappers>
        <mapper class="com.kuang.mapper.ActorInfoMapper"/>
    </mappers>
</configuration>
```



——com.kuang.pojo.ActorInfo.java

```
package com.kuang.pojo;

import lombok.Data;

@Data
public class ActorInfo {
    private String actor_id;
    private String name;
    private String name_en;
    private String img;
}
```

——com.kuang.mapper.ActorInfoMapper.java

```
package com.kuang.mapper;

import com.kuang.pojo.ActorInfo;

import java.util.List;

public interface ActorInfoMapper {
    public List<ActorInfo> selectActorInfo();
}
```

——com.kuang.mapper.ActorInfoMapper.xml

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="com.kuang.mapper.ActorInfoMapper">

    <select id="selectActorInfo" resultType="actorInfo">
        select * from actor_info;
    </select>
</mapper>
```

——最后测试类

```
import com.kuang.mapper.ActorInfoMapper;
import com.kuang.pojo.ActorInfo;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import java.io.IOException;
import java.io.InputStream;
import java.util.List;

public class Test {
    public static void main(String[] args) throws IOException {
        String resources = "mybatis-config.xml";
        InputStream in = Resources.getResourceAsStream(resources);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(in);
        SqlSession sqlSession = sqlSessionFactory.openSession(true);
        ActorInfoMapper actorInfoMapper = sqlSession.getMapper(ActorInfoMapper.class);
        List<ActorInfo> actorInfoList = actorInfoMapper.selectActorInfo();
        for (ActorInfo a :
                actorInfoList) {
            System.out.println(a.toString());
        }
    }
}
```

主要是通过Resources 的 getResourceAsStream 方法读写核心xml，

实例化SqlSessionFactoryBuilder，且打开它的openSession方法