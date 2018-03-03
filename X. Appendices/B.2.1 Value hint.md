### 附录B.2.1 值提示

每一个hint的`name`属性参考了property的`name`。在上面最初的例子里，我们为`spring.jpa.hibernate.ddl-auto`属性提供了5个值：`none`，`validate`，`update`，`create`和`create-drop`。每个值也可以有一个描述。

如果你的属性不是`Map`类型，你可以为key和value一起提供hint（但不是为map它自己）。特殊的`.keys`和`.values`后缀必须被分别地用于参考keys和values。

让我们假设一个`foo.contexts`，它把神奇的String值映射到一个Integer：
```java
@ConfigurationProperties("foo")
public class FooProperties {

    private Map<String,Integer> contexts;
    // getters and setters
}
```
例如，神奇的值是foo和bar。为了给key提供额外的内容帮助，你可以将以下内容添加到[模块的手工元数据](https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#configuration-metadata-additional-metadata)：
```json
{"hints": [
    {
        "name": "foo.contexts.keys",
        "values": [
            {
                "value": "foo"
            },
            {
                "value": "bar"
            }
        ]
    }
]}
```
**注** 当然，对那些有两个值的，你应当有一个替代的`Enum`。如果你的IDE支持，这是目前为止实现自动补全的最有效的方式。