# 一.什么是构建工具?
- 构建工具是一个把源代码生成可执行应用程序的过程自动化的程序（例如Android app生成apk）。构建包括编译、连接跟把代码打包成可用的或可执行的形式。
- 简单来说就是让项目变得自动化.

# 二.构建工具有哪些?
- 主流有Ant、Maven和Gradle。目前主流的是Maven和Gradle.

- Gradle是一个基于Apache Ant和Apache Maven概念的项目自动化构建开源工具,目前比较火.
- Apache Maven，是一个软件（特别是Java软件）项目管理及自动构建工具,是Apache 软件基金会独立的Apache项目.

# 三.Maven
## 1.maven的核心功能

- **坐标与依赖**
- **仓库**
- **生命周期与插件**
- **还有很多,就不讲了**

##2.坐标与依赖

> 为了能够自动化地解析任何一个Java构件, Maven必须将它们唯一标识, 这就是依赖管理的底层基础-坐标.

###2.1坐标
> 在数学中, 任何一个坐标可以唯一确定一个“点”.
> 任何一个构件都可以使用maven坐标进行唯一标识，

Maven 坐标为Java构件引入了秩序, 任何一个构件都必须明确定义自己的坐标, 坐标元素包括groupId、artifactId、version、packaging、classfier:

    <dependency>
        <groupId>org.apache.poi</groupId>
        <artifactId>poi</artifactId>
        <version>4.1.0</version>
    </dependency>

其中groupId、artifactId、version可以算作必要三元素了。
 | 元素 | 描述 
 | ---- | --- |
 | groupId | 定义当前模块隶属的实际Maven项目, 表示方式与Java包类似Maven项目隶属的实际项目，命名方式通常与域名反向一一对应。必须定义。
 |artifactId|实际项目中的一个Maven项目（模块），推荐使用实际项目名称作为artifactId的前缀。必须定义。
 |version|Maven项目当前所处的版本。必须定义。|
 |packaging|Maven项目的打包方式，打包方式通常与所生成构件的文件扩展名对应。当没有定义时，Maven会使用默认值jar。
 |classifier|帮助定义构件输出的一些附属附件。注意，不能直接定义项目的classifier，因为附属构件不是项目直接默认生成的，而是由附加的插件帮助生成的。

在上述5个元素中，groupId, artifactId, version是必选的，packaging是可选的，classfier是不能直接定义的。

###2.2依赖

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

###2.3 依赖范围

