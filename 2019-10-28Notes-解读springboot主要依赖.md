# Notes-解读springboot主要依赖
#### 作者:coresu    
#### 时间:2019-10-28


### pom文件解读   
#### 父项目： 
 ```java
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.0.RELEASE</version>
    </parent>
 ```
spring-boot-starter-parent类依赖于spring-boot-dependencies类
```java
  <parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.2.0.RELEASE</version>
    <relativePath>../../spring-boot-dependencies</relativePath>
  </parent>
```

spring-boot-dependencies类是真正来管理spring boot中的所有版本依赖，也称：版本控制中心。 
当在版本控制中心没有我们所需的版本依赖时，可以手动写入。   


#### starter倒入依赖   

```java
    <!-- Add typical dependencies for a web application -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```
spring-boot-starter-web类中可以看出依赖于很多组件，如下： 
```java
<dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter</artifactId>
      <version>2.2.0.RELEASE</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-json</artifactId>
      <version>2.2.0.RELEASE</version>
      <scope>compile</scope>
    </dependency>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-tomcat</artifactId>
      <version>2.2.0.RELEASE</version>
      <scope>compile</scope>
    </dependency>

    ......
    ......
```

当我们需要时就从start开始导入我们需要的功能，也称：场景启动器。    
spring boot将所有的功能场景抽离出来，当需要时引入相应场景依赖，boot会自动帮我们导入相关依赖。    


### @SpringBootApplication注解类解读     
```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Inherited
@SpringBootConfiguration   
@EnableAutoConfiguration
@ComponentScan(excludeFilters = { @Filter(type = FilterType.CUSTOM, classes = TypeExcludeFilter.class),
        @Filter(type = FilterType.CUSTOM, classes = AutoConfigurationExcludeFilter.class) })
@ConfigurationPropertiesScan
public @interface SpringBootApplication {
```
#### 什么是@SpringBootConfiguration
SpringBootApplication是程序启动的入口，调用main方法来启动spring boot应用。  
查看pringBootApplication类源文件可以看到是一段组合注解，   

@SpringBootConfiguration注解表示，spring boot定义的的一个配置类   
@Configuration表示在配置类上进行注解，是spring定义的一个注解配置类   

配置类和配合文件是一样的，即：满足功能所需依赖，配置类也是容器中的一个组件。 
#### 什么是@EnableAutoConfiguration
@EnableAutoConfiguration注解表示启动自动配置功能，springboot帮我们自动配置相关功能。

```java
@AutoConfigurationPackage
@Import(AutoConfigurationImportSelector.class)
public @interface EnableAutoConfiguration {
```
查看EnableAutoConfiguration类内部，可以看到两个注解：   
1. AutoConfigurationPackage自动配置包     
2. Import(AutoConfigurationImportSelector.class)  
Import属于spring的一个底层注解，表示给容器自动导入一个组件，导入组件的名字由括号中类名决定。

EnableAutoConfiguration的功能：将主配置类，也就是@SpringBootApplication所标注的类所在包及该包下所以子包中所有组件全部扫描至spring容器中，以供使用。   



#### 什么是AutoConfigurationImportSelector
AutoConfigurationImportSelector是导入组件的配置类选择器，将所需导入的组件以全类名的方式返回，并将这些组件添加到容器中；选择器会给组件添加很多的自动配置类注解（XXXAutoConfiguration），也就是给容器中导入场景所需的类，以这种方式实现自动化配置。  









