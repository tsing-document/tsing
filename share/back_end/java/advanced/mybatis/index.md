### 目录
#### 一、简介
#### 二、优势
#### 三、第一个应用
#### 四、XML配置
#### 五、XML映射文件
#### 六、动态SQL

### 一、简介

- 官网地址：[https://mybatis.org/mybatis-3/zh/sqlmap-xml.html]
- MyBatis 是一款优秀的持久层框架，它支持自定义 SQL、存储过程以及高级映射。MyBatis 免除了几乎所有的 JDBC 代码以及设置参数和获取结果集的工作。MyBatis 可以通过简单的 XML 或注解来配置和映射原始类型、接口和 Java POJO（Plain Old Java Objects，普通老式 Java 对象）为数据库中的记录。

### 二、优势

todo

### 三、第一个应用

- 1、添加依赖

    ```java
     <dependency>
         <groupId>org.mybatis</groupId>
         <artifactId>mybatis</artifactId>
         <version>3.5.5</version>
     </dependency>
     <dependency>
         <groupId>mysql</groupId>
         <artifactId>mysql-connector-java</artifactId>
         <version>8.0.22</version>
     </dependency>
    ```

- 2、创建`mybatis-config.xml`文件

    ```java
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE configuration
            PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-config.dtd">
    <configuration>
        <!-- 默认的环境ID：development：开发模式 work: 工作模式   -->
        <environments default="development">
            <!-- 每个environments元素定义的环境ID: id="development" -->
            <environment id="development">
                <!-- 事务管理器的配置：type="JDBC" -->
                <transactionManager type="JDBC"/>
                <!-- 三种内建的数据源类型：type=[ UNPOOLED | POOLED | JNDI ] -->
                <dataSource type="POOLED">
                    <property name="driver" value="com.mysql.cj.jdbc.Driver"/>
                    <property name="url" value="jdbc:mysql://xx.xx.xx.xx:3306/car?useUnicode=true;characterEncoding=utf-8"/>
                    <property name="username" value="xx"/>
                    <property name="password" value="xx"/>
                </dataSource>
            </environment>
        </environments>
        <mappers>
            <mapper resource="UserMapper.xml"/>
        </mappers>
    </configuration>
    ```

- 3、创建接口

    ```java
    public interface UserMapper {
        User getUser(String id);
    }
    ```

- 4、创建`UserMapper.XML`

    ```java
    <?xml version="1.0" encoding="UTF-8" ?>
    <!DOCTYPE mapper
            PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
            "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
    <mapper namespace="com.tsing.controller.UserMapper">
        <select id="getUser" resultType="com.tsing.controller.User">
            select * from user where id = #{id}
        </select>
    </mapper>
    ```

- 5、创建测试类

    ```java
    @Test
    public void test() throws IOException {
        String resource = "mybatis-config.xml";
        InputStream inputStream = Resources.getResourceAsStream(resource);
        SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
    
        SqlSession sqlSession = sqlSessionFactory.openSession();
        UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        User user = mapper.getUser("1");
        System.out.println(user);
    }
    ```

- 6、核心内容简介
  
    - 作用域（Scope）和生命周期
    - SqlSessionFactoryBuilder
    - SqlSessionFactory
    - SqlSession
    - 映射器实例

### 四、XML 配置

- properties文件

    - 外部动态引入配置文件替换属性值：

        - 1、创建`db.properties`文件

            ```properties
            driver=com.mysql.cj.jdbc.Driver
            url=jdbc:mysql://47.101.159.7:3306/car?useUnicode=true;characterEncoding=utf-8
            username=car
            password=h3Brk75ptnM6FG4e
            ```

        - 2、在`springmc-config.xml`中引入配置文件并修改动态替换值

            ```xml
            <?xml version="1.0" encoding="UTF-8" ?>
            <!DOCTYPE configuration
                    PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
                    "http://mybatis.org/dtd/mybatis-3-config.dtd">
            <configuration>
                <properties resource="db.properties" />
                <!-- 默认的环境ID：development：开发模式 work: 工作模式   -->
                <environments default="development">
                    <!-- 每个environments元素定义的环境ID: id="development" -->
                    <environment id="development">
                        <!-- 事务管理器的配置：type="JDBC" -->
                        <transactionManager type="JDBC"/>
                        <!-- 三种内建的数据源类型：type=[ UNPOOLED | POOLED | JNDI ] -->
                        <dataSource type="POOLED">
                            <property name="driver" value="${driver}"/>
                            <property name="url" value="${url}"/>
                            <property name="username" value="${username}"/>
                            <property name="password" value="${password}"/>
                        </dataSource>
                    </environment>
                </environments>
                <mappers>
                    <mapper resource="UserMapper.xml"/>
                </mappers>
            </configuration>
            ```

- setting

    - todo

​     

### 五、XML映射文件

- select
    - 配置项
        ```java
            <select
              id="selectPerson"
              parameterType="int"
              parameterMap="deprecated"
              resultType="hashmap"
              resultMap="personResultMap"
              flushCache="false"
              useCache="true"
              timeout="10"
              fetchSize="256"
              statementType="PREPARED"
              resultSetType="FORWARD_ONLY">
        ```
        
    - 案例：
    
        ```java
        //mapper接口
        public interface UserMapper {
            User getUser(String id);
        }
        
        //mapper映射文件
        <?xml version="1.0" encoding="UTF-8" ?>
        <!DOCTYPE mapper
                PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
                "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
        <mapper namespace="com.tsing.mapper.UserMapper">
            <select id="getUser"
                    parameterType="String"
                    resultType="com.tsing.pojo.User"
                    flushCache="true"
                    useCache="true">
                select * from user where id = #{id}
            </select>
        </mapper>
        
        <!--
        select配置：
            1. id="getUser" 在命名空间中的唯一的标识符。
            2. parameterType="String" 传入语句的参数的类全限定名或别名。
            3. resultType="com.tsing.pojo.User" 返回的类的全限定名，注意：返回的结果是集合，应该设置为集合包含的类型，而不是集合本身。
            4. resultMap
            5. flushCache="true" 默认值：false。只要语句被调用，都会导致本地缓存和二级缓存被清空。
            6. useCache="true" 将其设置成true，将会导致本条语句的结果欸二级缓存缓存起来，默认值：对select元素为true。
            7. statementType：
            8. resultSetType
            9. resultOrdered
        -->
        ```
    
        
    
- insert、update和delete

    - 配置项

        ```java
        <insert
          id="insertAuthor"
          parameterType="domain.blog.Author"
          flushCache="true"
          statementType="PREPARED"
          keyProperty=""
          keyColumn=""
          useGeneratedKeys=""
          timeout="20">
        
        <update
          id="updateAuthor"
          parameterType="domain.blog.Author"
          flushCache="true"
          statementType="PREPARED"
          timeout="20">
        
        <delete
          id="deleteAuthor"
          parameterType="domain.blog.Author"
          flushCache="true"
          statementType="PREPARED"
          timeout="20">
        ```

    - 案例：

        ```java
        //mapper接口
        public interface UserMapper {
            User getUser(String id);
            void insertUser();
            void updateUser(User user);
            void deleteUserById(String id);
            void batchInsertUser(List<User> list);
        }
        
        //mapper映射文件
        <mapper namespace="com.tsing.mapper.UserMapper">
            //新增
            <insert id="insertUser">
                INSERT INTO user (
                    id,
                    name,
                    passwd,
                    city_name,
                    city_code,
                    account,
                    phone,
                    is_enable
                )
                VALUES
                (
                    '12',
                    '青衣',
                    '12',
                    '北京',
                    '111111',
                    '22222',
                    '15150594533',
                    '0'
                );
            </insert>
                
            <!-- 批量插入数据 -->
            <insert id="batchInsertUser">
                INSERT INTO user ( id, name)
                VALUES
                <foreach item="item" collection="list" separator=",">
                    (#{item.name}, #{item.id})
                </foreach>
            </insert>
                
        	//修改
            <update
                    id="updateUser"
                    parameterType="com.tsing.pojo.User">
                update user
                <set>
                    name = #{name}
                </set>
                    where id = #{id}
            </update>
        	
            //删除
            <delete id="deleteUserById">
                delete from user where id = #{id}
            </delete>
        </mapper>
                
        //测试类
            @Test
            public void testInsert() throws IOException {
                String resource = "mybatis-config.xml";
                InputStream inputStream = Resources.getResourceAsStream(resource);
                SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        
                SqlSession sqlSession = sqlSessionFactory.openSession();
                UserMapper mapper = sqlSession.getMapper(UserMapper.class);
                mapper.insertUser();
                sqlSession.commit();
                sqlSession.close();
            }
        
            @Test
            public void testUpdate() throws IOException {
                String resource = "mybatis-config.xml";
                InputStream inputStream = Resources.getResourceAsStream(resource);
                SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        
                SqlSession sqlSession = sqlSessionFactory.openSession();
                UserMapper mapper = sqlSession.getMapper(UserMapper.class);
        
                User u = new User();
                u.setName("修改后的数据");
                u.setId("12");
                mapper.updateUser(u);
                sqlSession.commit();
                sqlSession.close();
            }
        
            @Test
            public void testDelete() throws IOException {
                String resource = "mybatis-config.xml";
                InputStream inputStream = Resources.getResourceAsStream(resource);
                SqlSessionFactory sqlSessionFactory = new SqlSessionFactoryBuilder().build(inputStream);
        
                SqlSession sqlSession = sqlSessionFactory.openSession();
                UserMapper mapper = sqlSession.getMapper(UserMapper.class);
                mapper.deleteUserById("12");
                sqlSession.commit();
                sqlSession.close();
        	}
        ```
- 字符串替换
- 结果映射
- 
