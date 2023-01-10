## 方法一：在pom文件中指定要使用的存储库
这在构建概要文件内部和外部都支持
```xml
<project>
...
  <repositories>
    <repository>
      <id>my-repo1</id>
      <name>your custom repo</name>
      <url>http://jarsm2.dyndns.dk</url>
    </repository>
    <repository>
      <id>my-repo2</id>
      <name>your custom repo</name>
      <url>http://jarsm2.dyndns.dk</url>
    </repository>
  </repositories>
...
</project>
```
## 方法二：创建settings.xml
在`${user.home}/.m2/settings.xml`或者 `${maven.home}/conf/settings.xml`文件中创建profile

```xml
<settings>
 ...
 <profiles>
   // 第一个仓库地址
   <profile>
     <id>nexus</id>
     <repositories>
       <repository>
         <id>my-repo2</id>
         <name>your custom repo</name>
         <url>http://jarsm2.dyndns.dk</url>
       </repository>
     </repositories>
   </profile>
    // 第二个仓库地址
    <profile>
      <id>aliyun</id>
      <repositories>
        <repository>
          <id>aliyun</id>
          <url>https://maven.aliyun.com/repository/public</url>
          <releases><enabled>true</enabled></releases>
          <snapshots><enabled>true</enabled></snapshots>
        </repository>
      </repositories>
      <pluginRepositories>
        <pluginRepository>
          <id>aliyun</id>
          <url>https://maven.aliyun.com/repository/public</url>
          <releases><enabled>true</enabled></releases>
          <snapshots><enabled>true</enabled></snapshots>
        </pluginRepository>
      </pluginRepositories>
    </profile>      
 </profiles>
如果您在profiles 中指定 repository 存储库，
需要激活该特定profiles,我们通过在 activeProfiles 中进行配置
 <activeProfiles>
   <activeProfile>nexus</activeProfile>
   <activeProfile>aliyun</activeProfile>
 </activeProfiles>
 ...
</settings>
```
你也可以通过执行以下命令来激活这个配置文件:
`mvn -Pnexus ...`
正常maven 的settings.xml配置完成profiles之后,可以在idea中进行切换
