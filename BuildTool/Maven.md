# Maven

## 简介

+ [Maven是基于项目对象模型（POM），可以通过一小段项目描述信息来管理项目的构建、报告和文档的软件项目管理工具](https://www.cnblogs.com/whgk/p/7112560.html)

- [官网](http://maven.apache.org)

- [setting.xml配置文件详解](https://www.cnblogs.com/yanghongfei/p/6995613.html)

## 命令

```
mvn     -v                //查看maven版本
        compile       //编译
        test             //测试
        package     //打包
        clean          //删除target
        install         //安装jar到本地仓库
```

## 本地仓库、远程仓库和镜像仓库

### 远程仓库地址的位置

+ maven\lib\maven-model-builder-3.6.1.jar的pom.xml文件中

 ### 修改镜像仓库

+ 在maven\conf\settings.xml中的mirrors标签

### 更改本地仓库的位置

+ 默认位置：C:\Users\用户名\.m2中

+ 修改方法：在maven\conf\settings.xml中的localRepository标签

## 生命周期和插件

### Maven生命周期

我们在开发项目的时候，我们不断地在经历编译、测试、打包、部署等过程，maven的生命周期就是对所有这些过程的一个抽象与统一，她的生命周期包含项目的清理、初始化、编译、测试、打包、集成测试、验证、部署、站点生成等几乎所有的过程，而且maven的生命周期是及其灵活，她生命周期的每个阶段是通过插件来实现的，maven也内置了很多插件，所以我们在项目进行编译、测试、打包的过程是没有感觉到。像编译是通过maven-compile-plugin实现的、测试是通过maven-surefire-plugin实现的。

Maven有三套相互独立的生命周期，请注意这里说的是“三套”，而且“相互独立”，初学者容易将Maven的生命周期看成一个整体，其实不然。这三套生命周期分别是：

+ Clean Lifecycle  在进行真正的构建之前进行一些清理工作。

+ Default Lifecycle  构建的核心部分，编译，测试，打包，部署等等。

+ Site Lifecycle  生成项目报告，站点，发布站点。

它们是相互独立的，你可以仅仅调用clean来清理工作目录，仅仅调用site来生成站点。当然你也可以直接运行 **mvn clean install site**运行所有这三套生命周期。

每套生命周期都由一组阶段(Phase)组成，我们平时在命令行输入的命令总会对应于一个特定的阶段。比如，运行mvn clean，这个的clean是Clean生命周期的一个阶段。有点绕？要知道有Clean生命周期，也有clean阶段

Clean生命周期一共包含了三个阶段：

+ pre-clean  执行一些需要在clean之前完成的工作。

+ clean  移除所有上一次构建生成的文件。

+ post-clean  执行一些需要在clean之后立刻完成的工作。

Site生命周期的各个阶段：

+ pre-site  执行一些需要在生成站点文档之前完成的工作。

+ site  生成项目的站点文档。

+ post-site  执行一些需要在生成站点文档之后完成的工作，并且为部署做准备。

+ site-deploy  将生成的站点文档部署到特定的服务器上。

最后，来看一下Maven的最重要的Default生命周期，绝大部分工作都发生在这个生命周期中，这里，我只解释一些比较重要和常用的阶段：

- 1、validate
- 2、initialize
- 3、generate-sources
- 4、process-sources    处理项目主资源文件。一般来说，是对src/main/resources目录的内容进行变量替换等工作后，复制到项目输出的主classpath目录中。
- 5、generate-resources
- 6、process-resources    
- 7、compile    编译项目的源代码。一般来说，是编译src/main/java目录下的Java文件至项目输出的主classpath目录中。
- 8、process-classes
- 9、generate-test-sources 
- 10、process-test-sources    处理项目测试资源文件。一般来说，是对src/test/resources目录的内容进行变量替换等工作后，复制到项目输出的测试classpath目录中。
- 11、generate-test-resources
- 12、process-test-resources    
- 13、test-compile    编译项目的测试源代码。一般来说，是编译src/test/java目录下的Java文件至项目输出的测试classpath目录中。
- 14、process-test-classes
- 15、test    使用合适的单元测试框架运行测试。这些测试代码不会被打包或部署。
- 16、prepare-package
- 17、package    接受编译好的代码，打包成可发布的格式，如 JAR 。
- 18、pre-integration-test
- 19、integration-test
- 20、post-integration-test
- 21、verify
- 22、install    将包安装至本地仓库，以让其它项目依赖。
- 23、deploy    将最终的包复制到远程的仓库，以让其它开发人员与Maven项目使用。

基本上，根据名称我们就能猜出每个阶段的用途，关于阶段的详细解释以及其她阶段的解释，请[参考](http://maven.apache.org/guides/introduction/introduction-to-the-lifecycle.html)

### 命令行与生命周期

从命令行执行Maven任务的最主要方式就是调用Maven的生命周期阶段。需要注意的是，各个生命周期是相互独立的，而一个生命周期的阶段是有前后依赖关系的。下面以一些常见的Maven命令为例，解释其执行的生命周期阶段：

+ mvn clean：该命令调用clean生命周期的clean阶段。实际执行的阶段为clean生命周期的pre-clean和clean阶段。

+ mvn test：该命令调用default生命周期的test阶段。实际执行的阶段为default生命周期的validate、initialize等，直到test的所有阶段。这也解释了为什么在执行测试的时候，项目的代码能够自动得以编译。

+ mvn clean install：该命令调用clean生命周期的clean阶段和default生命周期的install阶段。实际执行的阶段为clean生命周期的pre-clean、clean阶段，以及default生命周期的从validate至install的所有阶段。该命令结合了两个生命周期，在执行正在的项目构建之前清理项目是一个很好的实践。

+ mvn clean deploy site-deploy：该命令调用clean生命周期的clean阶段、default生命周期的deploy阶段，以及site生命周期的site-deploy阶段。实际执行的阶段为clean生命周期的pre-clean、clean阶段，default生命周期的所有阶段，以及site生命周期的所有阶段。该命令结合了Maven所有三个生命周期，且deploy为default生命周期的最后一个阶段，site-deploy为site生命周期的最后一个阶段。

由于Maven中主要的生命周期阶段并不多，而常用的Maven命令实际都是基于这些阶段简单组合而成的，因此只要对Maven生命周期有一个基本的理解，读者就可以正确而熟练地使用Maven命令。

### Maven插件机制

+ [插件地址](http://maven.apache.org/plugins/index.html)

+ [war包生成插件配置](http://maven.apache.org/plugins/maven-war-plugin/examples/war-manifest-guide.html)

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-war-plugin</artifactId>
            <version>3.2.3</version>
            <executions>
                <execution>
                    <!--绑定生命周期的package阶段，在package阶段执行source这个插件-->
                    <phase>package</phase>
                    <goals>
                        <!--执行的目标-->
                        <goal>war</goal>
                    </goals>
                </execution>
            </executions>
            <configuration>
                <archive>
                    <manifest>
                        <addClasspath>true</addClasspath>
                    </manifest>
                </archive>
            </configuration>
        </plugin>
    </plugins>
</build>
```

## pom文件和依赖

### pom文件解析

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!--groupId是项目的包名,一般是反写的公司地址+项目名 -->
    <groupId>com.lucky.hellomaven</groupId>
    <!--artifactId是模块名，建议使用项目名 -->
    <artifactId>HelloMaven</artifactId>
    <!--version是版本号。第一个是大版本号，第二个是分支版本号，第三个表示小版本号
        snapshot 快照
        alpha 内测版
        beta 公测版本
        Release 稳定
        GA正式发布
     -->
    <version>1.0-SNAPSHOT</version>
    <!--不写默认是打包成jar，也可以war，zip或者pom-->
    <packaging>jar</packaging>
    <!--name为项目描述名-->
    <name>"学习"</name>
    <!--url为项目的地址-->
    <url></url>
    <!--表示项目的表示-->
    <description></description>
    <!--开发者-->
    <developers></developers>
    <!--许可信息-->
    <licenses></licenses>
    <!--组织信息-->
    <organization></organization>

    <!--dependencies表示依赖列表，可以包含多个依赖项（很重要）-->
    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <type></type>
            <!--指依赖的范围，以下表示只在test有用-->
            <scope>test</scope>
            <!--设置依赖是否可选，默认为false-->
            <optional>false</optional>
            <!--排除依赖传递列表-->
            <exclusions>
                <exclusion>
                    <artifactId></artifactId>
                    <groupId></groupId>
                </exclusion>
            </exclusions>
        </dependency>
    </dependencies>

    <!--依赖的管理-->
    <dependencyManagement>

    </dependencyManagement>

    <!--build为构建行为提供支持-->
    <build>
        <!--插件列表-->
        <plugins>
            <!--插件-->
            <plugin>
                <!--以下为打包插件-->
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.3</version>
                <executions>
                    <execution>
                        <!--绑定生命周期的package阶段，在package阶段执行source这个插件-->
                        <phase>package</phase>
                        <goals>
                            <!--执行的目标-->
                            <goal>war</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <archive>
                        <manifest>
                            <addClasspath>true</addClasspath>
                        </manifest>
                    </archive>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <parent></parent>
    <!--用来聚合多个maven模块的编译-->
    <modules></modules>
</project>
```

### 依赖范围（scope）

+ [详细介绍指定值](http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)

### 依赖传递

A依赖B，B依赖C，A默认在构建是会依赖与C，如果不要A依赖与C，则使用排除依赖列表进行排除

### 依赖冲突

如果有A和B依赖不同版本相同构建。

+ 短路优先（会优先简析短的版本）

+ 先声明先优先（如果声明路径相同，则谁先声明，先解析谁）

### 聚合和继承

+ 聚合（将多个maven项目放到一起运行）

使用modules标签进行聚合

+ 继承

多个项目同时依赖一个包，可以将该包的坐标提取出来放到一个父项目的pom中，使用dependencyManagement标签

子项目使用parent标签来定位到父项目的依赖