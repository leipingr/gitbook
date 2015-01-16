

# Magpie Archetype
-----------------

我们为大家提供了一个Magpie的Maven archetype（ 什么是<font color=red>[`archetype`](http://maven.apache.org/guides/introduction/introduction-to-archetypes.html) </font> ），通过archetype可以方便地创建一个依赖Magpie的demo工程，其中包括了完整可运行的demo代码，根据archetype创建demo工程的步骤如下：

## 1. 首先在~/.m2/setting.xml中配置nexus服务器信息：

```xml
<mirrors>
    <mirror>
        <id>nexus</id>
        <mirrorOf>*</mirrorOf>
        <url>http://172.18.64.96:8080/nexus/content/groups/public/</url>
    </mirror>
</mirrors>
```

### 2. 在终端执行命令，并根据命令提示操作:

```java
mvn archetype:generate -DarchetypeGroupId=com.unionpay.magpie \
                       -DarchetypeArtifactId=magpie-archetype-quickstart \
                       -DarchetypeVersion=1.1.0.Beta7
```


>注意：
上述命令中的<font color=red> `1.1.0.Beta7`</font> 表示<font color=red>`magpie archetype`</font>的发布版本号。请查询 Nexus开发库 ，使用最新的magpie archetype版本号。
