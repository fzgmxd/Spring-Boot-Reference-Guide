### 附录 E.1.1 可执行jar文件结构

Spring Boot Loader兼容的jar文件应该遵循以下结构：

```java
example.jar
 |
 +-META-INF
 |  +-MANIFEST.MF
 +-org
 |  +-springframework
 |     +-boot
 |        +-loader
 |           +-<spring boot loader classes>
 +-BOOT-INF
    +-classes
    |  +-mycompany
    |     +-project
    |        +-YourClasses.class
    +-lib
       +-dependency1.jar
       +-dependency2.jar
```
应用类需要放在内嵌的`BOOT-INF/classes`目录下。依赖需要放在内嵌的`BOOT-INF/lib`目录下。
