### 附录B.2.1 值提示

每一个hint的`name`属性参考了property的`name`。在[上面最初的例子](https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#configuration-metadata-format)里，我们为`spring.jpa.hibernate.ddl-auto`属性提供了5个值：`none`、`validate`、`update`、`create`和`create-drop`。每个值也可以有一个描述。

如果你的属性不是`Map`类型，你可以为key和value一起提供hint（但不是为map它自己）。特殊的`.keys`和`.values`后缀必须被分别地用于参考keys和values。

让我们假设一个`sample.contexts`，它把神奇的String值映射到一个Integer：
```java
@ConfigurationProperties("sample")
public class SampleProperties {

	private Map<String,Integer> contexts;
	// getters and setters
}
```
例如，神奇的值是`sample1`和`sample2`。为了给key提供额外的内容帮助，你可以将以下内容添加到[模块的手工元数据](https://docs.spring.io/spring-boot/docs/2.0.0.RELEASE/reference/htmlsingle/#configuration-metadata-additional-metadata)：
```json
{"hints": [
	{
		"name": "sample.contexts.keys",
		"values": [
			{
				"value": "sample1"
			},
			{
				"value": "sample2"
			}
		]
	}
]}
```
**注** 我们建议你对这两个值使用`Enum`。如果你的IDE支持，这是目前为止实现自动补全的最有效的方式。