# MyBatisPlus

## 一、环境


**pom文件**  
`<version>` 大于2的需要指定驱动为【`driver-class-name: com.mysql.cj.jdbc.Driver`】
~~~
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.5.6</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

~~~


**启动类开启MapperScan注解**
~~~
@MapperScan(value = "com.loong.mpdemo.mapper")

~~~


**实体类的主键id**
~~~
@TableId(value = "id", type = IdType.AUTO)
value = "id"代表类型是主键
type = IdType.AUTO代表自增长

~~~


**Mapper接口**  
`继承BaseMapper`
~~~
public interface DeptMapper extends BaseMapper<Dept> {
}

~~~


**在yml中配置日志**
~~~
mybatis-plus:
  configuration:
    log-impl: org.apache.ibatis.logging.stdout.StdOutImpl

~~~


## 二、CRUD
~~~

~~~


## 三、表和列


### 1、主键类型
~~~
@TableId(value = "id" , type = Idtype.AUTO)
Idtype
  auto 自动增长
  id_worker 实体类使用Long 表使用bigint 雪花算法，分布式ID
  ......
~~~


### 2、指定表名
~~~
@TableName(value = "user")
指定user表

~~~


### 3、指定列名
~~~
@TableField(value = "name)
指定name字段列

~~~


### 4、驼峰命名
~~~
数据库字段推荐使用user_name形式

~~~


## 四、自定义sql
~~~



~~~


## 五、查询和分页
1、查询构造器Wrapper
~~~
allEq
  传入Map类型
  Map中有key的value是null 使用allEq(param, true)    true 加入is null
                                          false         忽略条件

eq
  等同于=

ne
  即!=

gt
  即>

ge
  >=

lt
  <

le
  <=

between
  between- ? and ?
  >=  <=
  闭区间

notBetween
  > <
  开区间

like , notLike
like "%值%"
notLike "%值%"

likeLeft, likeRight
liekLeft "%值"  值在结尾
likeRight "值%" 值在开头

......


~~~

2、分页
**配置分页注解类**
~~~
旧版分页
@Configuration
public class Config {
    /**
     * 定义方法，返回的值是 java 对象，这个对象是放入到 spring 容器中
     */
    @Bean
    public PaginationInterceptor paginationInterceptor() {
        return new PaginationInterceptor();
    }
}

最新版分页 3.4.2
    @Bean
    public MybatisPlusInterceptor mybatisPlusInterceptor() {
        MybatisPlusInterceptor interceptor = new MybatisPlusInterceptor();
        interceptor.addInnerInterceptor(new PaginationInnerInterceptor(DbType.H2));
        return interceptor;
    }

~~~



## 六、MP生成器

**配置**
~~~
<!--        模板引擎-->
<dependency>
    <groupId>org.apache.velocity</groupId>
    <artifactId>velocity-engine-core</artifactId>
    <version>2.3</version>
</dependency>

<!--        代码生成器-->
<dependency>
    <groupId>com.baomidou</groupId>
    <artifactId>mybatis-plus-generator</artifactId>
    <version>3.3.2</version>
</dependency>

~~~
