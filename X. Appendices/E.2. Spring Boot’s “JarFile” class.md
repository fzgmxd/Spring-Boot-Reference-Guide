### 附录 E.2. Spring Boot的"JarFile"类

Spring Boot用于支持加载内嵌jars的核心类是`org.springframework.boot.loader.jar.JarFile`。它允许你从一个标准的jar文件或内嵌的子jar数据中加载jar内容。当首次加载的时候，每个`JarEntry`]=\的位置被映射到一个偏移于外部jar的物理文件：
```java
myapp.jar
+-------------------+-------------------------+
| /BOOT-INF/classes | /BOOT-INF/lib/mylib.jar |
|+-----------------+||+-----------+----------+|
||     A.class      |||  B.class  |  C.class ||
|+-----------------+||+-----------+----------+|
+-------------------+-------------------------+
 ^                    ^           ^
 0063                 3452        3980
```
上面的示例展示了如何在`myapp.jar`的`/BOOT-INF/classes`里找到`A.class`，也就是位置`0063`。来自于内嵌jar的`B.class`实际可以在`myapp.jar`的`3452`处找到，`B.class`可以在`3980`处找到。
有了这些信息，我们就可以通过简单的寻找外部jar的合适部分来加载指定的内嵌实体。我们不需要解压存档，也不需要将所有实体读取到内存中。
