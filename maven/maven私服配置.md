#### 首先修改本地maven的settings.xml配置,使用maven私有库

##### 在server节点里面添加
    
    <server>   
        <id>nexus-releases</id>    
        <username>admin</username>    
        <password>admin123</password>    
    </server>    
    <server>    
        <id>nexus-snapshots</id>    
        <username>admin</username>    
        <password>admin123</password>    
    </server>

##### 在mirrors节点里面新建

    <mirror>     
        <id>nexus-releases</id>     
        <mirrorOf>*</mirrorOf>     
        <url>http://192.168.50.106:8081/repository/maven-public/</url>     
    </mirror>    
    <mirror>     
        <id>nexus-snapshots</id>     
        <mirrorOf>*</mirrorOf>     
        <url>http://192.168.50.106:8081/repository/maven-releases/</url>     
    </mirror>

##### 在profiles节点里面新建

    <profile>
        <id>nexus</id>
        <repositories>
            <repository>
                <id>nexus-releases</id>
                <url>http://nexus-releases</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </repository>
            <repository>
                <id>nexus-snapshots</id>
                <url>http://nexus-snapshots</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </repository>
        </repositories>
        <pluginRepositories>
            <pluginRepository>
                <id>nexus-releases</id>
                <url>http://nexus-releases</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </pluginRepository>
            <pluginRepository>
                <id>nexus-snapshots</id>
                <url>http://nexus-snapshots</url>
                <releases><enabled>true</enabled></releases>
                <snapshots><enabled>true</enabled></snapshots>
            </pluginRepository>
        </pluginRepositories>
    </profile>

##### 新增一个activeProfiles节点，该节点和profiles节点一个层次

    <activeProfiles>
        <activeProfile>nexus</activeProfile>
    </activeProfiles>
以上就是settings.xml配置.

##### 开始项目配置,在父pom里面,添加节点,跟dependencies节点平级
    
    <!--下载-->
    <repositories>
        <repository>
            <id>maven-central</id>
            <name>maven-central</name>
            <url>http://192.168.50.106:8081/repository/maven-central/</url>
            <!--snapshots默认是关闭的,需要开启  -->
            <snapshots>
                <enabled>true</enabled>
            </snapshots>
            <releases>
                <enabled>true</enabled>
            </releases>
        </repository>
    </repositories>

然后刷新项目,就开始下载服务器的jar包了.


