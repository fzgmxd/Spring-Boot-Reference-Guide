### 附录B.1.2. Property属性

`properties`数组中包含的JSON对象可由以下属性构成：

|名称|类型|目的|
|----|:----|:----|
|`name`|String|property的全名，格式为小写虚线分割的形式（比如`server.servlet.path`）。该属性是强制性的|
|`type`|String|property数据类型的完整的签名。例如`java.lang.String`，但也可以是一个完整的泛型类，比如`java.util.Map<java.util.String,acme.MyEnum>`。该属性可以用来指导用户他们可以输入值的类型。为了保持一致，原生类型使用它们的包装类代替，比如`boolean`变成了`java.lang.Boolean`。注意，这个类可能是个从一个字符串转换而来的复杂类型。如果类型未知则该属性会被忽略|
|`description`|String|一个简短的组的描述，用于展示给用户。如果没有描述可用则该属性会被忽略。推荐使用一个简短的段落描述，开头提供一个简洁的总结，最后一行以句号结束|
|`sourceType`|String|贡献property的来源类名。例如，如果property来自一个被`@ConfigurationProperties`注解的类，该属性将包括该类的全限定名。如果来源类型未知则该属性会被忽略|
|`defaultValue`|Object|当property没有定义时使用的默认值。如果property类型是个数组则该属性也可以是个数组。如果默认值未知则该属性会被忽略|
|`deprecated`|Deprecation|指定该property是否过期。如果该字段没有过期或该信息未知则该属性会被忽略。更多细节请查看下面|

每一个`properties`的`deprecation`属性包含的JSON对象可以包含如下的属性：

|名称|类型|目的|
|----|:----|:----|
|`level`|String|The level of deprecation, can be either warning (default) or error. When a property has a warning deprecation level it should still be bound in the environment. When it has an error deprecation level however, the property is no longer managed and will not be bound.|
|`reason`|String|A short description of the reason why the property was deprecated. May be omitted if no reason is available. It is recommended that descriptions are a short paragraphs, with the first line providing a concise summary. The last line in the description should end with a period (.).|
|`replacement`|String|The full name of the property that is replacing this deprecated property. May be omitted if there is no replacement for this property.|

**注** Prior to Spring Boot 1.3, a single deprecated boolean attribute can be used instead of the deprecation element. This is still supported in a deprecated fashion and should no longer be used. If no reason and replacement are available, an empty deprecation object should be set.
Deprecation can also be specified declaratively in code by adding the @DeprecatedConfigurationProperty annotation to the getter exposing the deprecated property. For instance, let’s assume the app.foo.target property was confusing and was renamed to app.foo.name
```java
@ConfigurationProperties("app.foo")
public class FooProperties {

    private String name;

    public String getName() { ... }

    public void setName(String name) { ... }

    @DeprecatedConfigurationProperty(replacement = "app.foo.name")
    @Deprecated
    public String getTarget() {
        return getName();
    }

    @Deprecated
    public void setTarget(String target) {
        setName(target);
    }
}
```
**注** There is no way to set a level as warning is always assumed since code is still handling the property.

The code above makes sure that the deprecated property still works (delegating to the name property behind the scenes). Once the getTarget and setTarget methods can be removed from your public API, the automatic deprecation hint in the meta-data will go away as well. If you want to keep a hint, adding manual meta-data with an error deprecation level ensures that users are still informed about that property and is particularly useful when a replacement is provided.