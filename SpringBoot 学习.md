# SpringBoot 学习

### 1. 编写主程序

```java
/**
*springBoot启动程序
*/

@SpringBootApplication  //必须声明，spring程序入口
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);  //主程序入口，传参
    }
}
```

> .run传入的类必须是@springBootApplication所标注的类

### 2. 部署

``` 
只需要导入一个插件，就可以自动的部署，不再需要springboot配置
```

将应用打成jar包即可

## 1. HelloWorld探究

### 1. pom文件解析

#### 1. 父项目

```xml
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.3.0.RELEASE</version>
    <relativePath/> <!-- lookup parent from repository -->
</parent>

他的父项目为
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-dependencies</artifactId>
    <version>2.3.0.RELEASE</version>
  </parent>
来真正管理SpringBoot里面的所有依赖版本；
```

Spring Boot版本仲裁中心

从而导入以来不需要版本，而没有版本管理的要需要声明版本号

#### 2. 启动器（starter）

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

spring-boot-starter-web：

​	spring-boot-starter场景启动器；帮我们导入了web模块正常运行需要的组件

> spring-boot-starter里面有更多的启动器

Spring Boot将所有的功能场景抽取出来，做成一个个starters（启动器），只需要在项目中引用就可以

### 2. 主程序类 ，主入口类

~~~java 
/**
*springBoot启动程序
*/

@SpringBootApplication  //必须声明，spring程序入口
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);  //主程序入口，传参
    }
}
~~~

**@SpringBootApplication**： 这个注解标注在某个类上说明是SpringBoot的主配置类，SpringBoot就应该运行这个类的main方法来启动SpringBoot应用

**@SpringBootConfiguration**：SpringBoot配置类

​		标注在某个类上，表示这是SpringBoot的配置类

**@EnableAutoConfiguration**： 开启自动配置功能 

**@import()**： 给容器中导入组件