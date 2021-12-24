# MyBatisPlus

## 一、环境
**version 大于2的**需要指定驱动为【`driver-class-name: com.mysql.cj.jdbc.Driver`】
~~~
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.5.6</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

~~~


**开启MapperScan注解**
~~~
@MapperScan(value = "com.loong.mpdemo.mapper")

~~~


**实体类的主键id**
~~~
@TableId(value = "id", type = IdType.AUTO)

~~~
