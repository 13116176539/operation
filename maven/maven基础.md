# 一.什么是构建工具?
- 构建工具是一个把源代码生成可执行应用程序的过程自动化的程序（例如Android app生成apk）。构建包括编译、连接跟把代码打包成可用的或可执行的形式。
- 简单来说就是让项目变得自动化.

# 二.构建工具有哪些?
- 主流有Ant、Maven和Gradle。目前主流的是Maven和Gradle.

- Gradle是一个基于Apache Ant和Apache Maven概念的项目自动化构建开源工具,目前比较火.它使用一种基于Groovy的特定领域语言来声明项目设置，而不是传统的XML。
- Apache Maven，是一个软件（特别是Java软件）项目管理及自动构建工具,是Apache 软件基金会独立的Apache项目.

# 三.Maven
## 1.maven的核心功能

- **坐标与依赖**
- **仓库**
- **生命周期**
- **还有很多,就不讲了**

## 2.坐标与依赖

> 为了能够自动化地解析任何一个Java构件, Maven必须将它们唯一标识, 这就是依赖管理的底层基础-坐标.

### 2.1坐标
> 在数学中, 任何一个坐标可以唯一确定一个“点”.
> 任何一个构件都可以使用maven坐标进行唯一标识，

Maven 坐标为Java构件引入了秩序, 任何一个构件都必须明确定义自己的坐标, 坐标元素包括groupId、artifactId、version、packaging、classfier:

    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi</artifactId>
        <version>4.1.0</version>
    </dependency>

其中groupId、artifactId、version可以算作必要三元素了。

 | 元素 | 描述 |
 | ---- | --- |
 | groupId | 定义当前模块隶属的实际Maven项目, 表示方式与Java包类似Maven项目隶属的实际项目，命名方式通常与域名反向一一对应。必须定义。
 |artifactId|实际项目中的一个Maven项目（模块），推荐使用实际项目名称作为artifactId的前缀。必须定义。
 |version|Maven项目当前所处的版本。必须定义。|
 |packaging|Maven项目的打包方式，打包方式通常与所生成构件的文件扩展名对应。当没有定义时，Maven会使用默认值jar。
 |classifier|帮助定义构件输出的一些附属附件。注意，不能直接定义项目的classifier，因为附属构件不是项目直接默认生成的，而是由附加的插件帮助生成的。

在上述5个元素中，groupId, artifactId, version是必选的，packaging是可选的，classfier是不能直接定义的。

### 2.2依赖

在pom中定义project下的dependencies元素可以包含一个或者多个dependency元素来声明一个或者多个项目依赖。

|元素 | 描述|
|---|---|
|groupId, artifactId, version|依赖的基本坐标
|type|依赖的类型，对应于坐标的packaging，默认jar|
|scope|	依赖的范围,用来控制依赖与三种classpath(编译classpath、测试classpath、运行classpath)的关系
|optional|标记依赖是否可选|
|exclusions|用来排除传递性依赖|

    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>4.2.7.RELEASE</version>

        <type>jar</type>
        <scope>compile</scope>
        <optional>false</optional>
        <exclusions>
            <exclusion>
                <groupId>log4j</groupId>
                <artifactId>log4j</artifactId>
            </exclusion>
        </exclusions>
    </dependency>

>Maven提供了dependency插件可以对Maven项目依赖查看以及优化, 如$ mvn dependency:tree可以查看当前项目的依赖树, 详见$ mvn dependency:help.

### 2.3 依赖范围

- maven在编译项目主代码时需要使用一套classpath，编译项目主代码时需要用到的jar包会以依赖的方式被引入到classpath中。

- maven在编译和执行测试这两个阶段会使用不同的classpath。

依赖范围就是用来控制与这三种classpath（编译classpath，测试classpath，运行classpath）的关系。maven中有以下几种依赖范围：

|依赖范围 | 含义|
|---|---|
|compile|编译依赖范围，默认范围。对于编译，测试，运行三种classpath都有效。
|test|测试依赖范围。只对于测试classpath有效，在编译主代码和运行主程序中不会被用到。例如junit
|provided|已提供依赖范围。对于编译和测试classpath有效，但在运行时无效。例如servlet-api|
|runtime|运行时编译依赖，对于测试和运行classpath有效，但在编译主代码时无效。例如数据库驱动。|
|system|系统依赖范围，和provided依赖范围完全一致，但必须通过systemPath显示指定依赖范围的路径，往往与本机系统绑定，谨慎使用
|import|导入依赖范围。不会对三种classpath有影响。

## 3.仓库

>maven中任何一个依赖，插件或者项目构建的输出，都可以称为构件。

在不是用maven的项目中，我们往往发现每个项目中都包含类似/lib的目录用来存储依赖的jar包，而且各个项目的lib包往往包含重复的内容。

maven项目使用任何一个构件的方式都是完全相同的，maven可以在某个位置统一存储所有maven共享的构件，这个统一的位置便是仓库。

### 3.1 仓库的分类

对于maven来说，仓库只分为两类： **本地仓库和远程仓库。** 

当maven根据坐标寻找构件的时候，它首先会查看本地仓库，如果本地仓库存在，直接使用；如果本地仓库不存在，需要查看是否有更新的构件版本，maven就会去远程仓库寻找，发现需要的构件之后，下载到本地仓库再使用。如果都没有找到，maven会报错。

中央仓库是maven核心自带的远程仓库，包含了绝大多数开源的构件。默认配置下，本地仓库没有maven需要的构件，它会尝试从中央仓库中寻找。

私服是另一种特殊的远程仓库，为了节省网络带宽和下载时间，应该在局域网中架设一个私有的仓库服务器，用来代理所有外部的远程仓库。

**本地仓库**
- 一般在maven项目中不存在类似/lib这样用来存放依赖文件的目录。当使用maven执行编译或者测试时，如果需要使用依赖文件，总是基于坐标使用本地仓库的依赖文件。
- 本地仓库的默认目录是：用户名/.m2/repository，如果用户需要自定义的仓库目录，编辑~/.m2/settings.xml，设置localRepository即可。
- 默认情况下~/.m2/settings.xml是不存在的，用户需要从maven安装目录复制$M2_HOME/conf/settings.xml文件再进行编辑。
- 一个构件只有在本地仓库中之后，才能由其他maven项目使用。
  
**远程仓库**
- 安装完成maven之后，如果没有执行任何maven命令，本地仓库目录是不存在的。当maven无法从本地仓库中找到需要的构件的时候，就会从远程仓库下载构件至本地仓库。对于maven来说，每个用户只有一个本地仓库，但是可以配置多个远程仓库。

- 中央仓库就是一个默认的远程仓库，maven的安装文件自带了中央仓库的配置。
- Maven内置了远程公用仓库：http://repo1.maven.org/maven2

**私服**
- 私服是一种特殊的远程仓库，架设在局域网内的仓库服务，私服代理广域网上的远程仓库，供局域网内的maven用户使用。
- 当maven需要下载构件的时候，从私服请求，如果私服上不存在此构件，则从外部的远程仓库中下载，缓存在私服之后，再为maven下载请求提供服务。此外，一些无法从外部仓库中下载到的构件也能从本地上传到私服供大家使用。
- 使用私服能够带来如下好处：
    节省网络（外网）带宽；
    加速maven构建；
    部署第三方构建：特指一些构件不能从远程仓库中获得；
    提供稳定性，增强控制；
    降低中央仓库的负荷；

## 4.Maven生命周期

>[《Maven进阶》1.maven 项目生命周期与构建原理](https://blog.csdn.net/luanlouis/article/details/50492163)

