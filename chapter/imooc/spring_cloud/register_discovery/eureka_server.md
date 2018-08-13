# Eureka Server

> eureka
> int. 有了！；找到了！
> n. (Eureka)人名；(西)欧雷卡


## 一个项目

使用 ui 创建，选择 Cloud Discovery -> Eureka Server 即可

以下是确认后默认生成的 eureka/build.gradle
```
buildscript {
	ext {
		springBootVersion = '2.0.4.RELEASE'
	}
	repositories {
		mavenCentral()
	}
	dependencies {
		classpath("org.springframework.boot:spring-boot-gradle-plugin:${springBootVersion}")
	}
}

apply plugin: 'java'
apply plugin: 'eclipse'
apply plugin: 'org.springframework.boot'
apply plugin: 'io.spring.dependency-management'

group = 'cn.mrcode.imooc.spring.cloud'
version = '0.0.1-SNAPSHOT'
sourceCompatibility = 1.8

repositories {
	mavenCentral()
}


ext {
	springCloudVersion = 'Finchley.SR1'
}

dependencies {
	compile('org.springframework.cloud:spring-cloud-starter-netflix-eureka-server')
	testCompile('org.springframework.boot:spring-boot-starter-test')
}

dependencyManagement {
	imports {
		mavenBom "org.springframework.cloud:spring-cloud-dependencies:${springCloudVersion}"
	}
}

```

关于版本：可以查看官网 http://projects.spring.io/spring-cloud/

```
第一行是cloud的版本，下面的是依赖的所有组件的版本号；
有多种版本号，是伦敦地铁的名称，按字母升序来表示由低到高的版本变化

Component	Edgware.SR4	Finchley.SR1	Finchley.BUILD-SNAPSHOT
spring-cloud-aws	1.2.3.RELEASE	2.0.0.RELEASE	2.0.1.BUILD-SNAPSHOT
```

## 启动
初始化的项目，只要增加一个 @EnableEurekaServer  注解即可启动。访问 http://localhost:8080/ 能看到 eureka的页面

```java
@SpringBootApplication
@EnableEurekaServer  
public class EurekaApplication {

	public static void main(String[] args) {
		SpringApplication.run(EurekaApplication.class, args);
	}
}
```

但是控制台一直报错：`com.netflix.discovery.shared.transport.TransportException: Cannot execute request on any known server`

原因是；