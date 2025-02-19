---
title: Maven
date: 2025-02-13 10:46:57
tags: [杂项, Maven]
---
# Maven

### 1.安装与IDEA使用
不赘述
### 2.依赖管理
#### 1.简介

Maven使用pom.xml文件来定义项目依赖。  
依赖的坐标
- GroupId：组织或项目的唯一标识符，通常用反向域名命名
- ArtifactId：项目或依赖名称。同组中有唯一性。
- Version：版本号
- Packaging：打包类型  
```java
//一个依赖示例
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-web</artifactId>
  <version>2.5.4</version>
</dependency>
```
依赖管理
~~~java
//properties设置版本号
//dependencyManagement管理依赖
  <properties>
     <spring-version>6.0.6</spring-version>  
    </properties>
  <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework</groupId>
                <artifactId>spring-context</artifactId>
                <version>${spring-version}</version>
            </dependency>
        </dependencies>
     </dependencyManagement>
~~~
依赖冲突:项目A依赖库B，B依赖C版本，A依赖C另一版本。Maven采取**最近路径优先策略**，选择离项目最近的一项，若距离相同则根据POM文件声明顺序。
### 3.构建管理
#### 生命周期
- validate：验证项目是否正确和所有必要信息是否可用。
- compile：编译项目的源代码。
- test：使用适当的单元测试框架（如 JUnit）测试编译好的代码。
- package：将编译后的代码打包成可分发的格式（如 JAR、WAR）。
- verify：运行任何集成测试来验证软件包的有效性。
- install：将软件包安装到本地 Maven 仓库，以供本地项目使用。
- deploy：将最终的构建结果复制到远程仓库，以供其他开发人员和项目共享。

### 4.Maven继承
**子项目继承父项目的配置**。通过继承机制，子项目可以复用父项目定义的依赖、插件、属性等配置，减少重复配置，提高项目的**可维护性**。
~~~java
<parent></parent>
~~~
### 5.Maven聚合
聚合是指在**一个父项目中管理多个子项目**，使得构建和管理多个模块变得更加方便。在**聚合项目**的根目录中运行 Maven 命令，可以同时构建和管理所有子项目。  
聚合项目（Aggregator Project）**本身通常不包含代码**，仅用于组织和管理子项目
聚合项目的 POM 文件通过 `<modules>`  元素定义了包含的子项目。通过聚合，可以一次性构建和管理所有子项目。简化了构建和发布过程。
  ~~~
  <modules>
    <module></module>
  </modules>
  ~~~
  
