### 附录B.1.4. 可重复的元数据节点

在同一个元数据文件中可以有多个"property"和"group"名称都相同的对象。例如，Spring Boot将`spring.datasource`属性绑定到Hikari，Tomcat和DBCP类，并且每个都潜在的提供了重复的属性名。虽然多次出现在元数据中的相同名称不应该是常见的，但是元数据的使用者应该注意确保他们支持它。
