### 附录B.1.2. Property属性

`properties`数组中包含的JSON对象可以包含以下属性：

|名称|类型|目的|
|----|:----|:----|
|`name`|String|property的全名，格式为小写虚线分割的形式（比如`server.servlet.path`）。该属性是强制性的|
|`type`|String|property数据类型的完整的签名。例如`java.lang.String`，但也可以是一个完整的泛型类，比如`java.util.Map<java.util.String,acme.MyEnum>`。该属性可以用来指导用户他们可以输入值的类型。为了保持一致，原生类型使用它们的包装类代替，比如`boolean`变成了`java.lang.Boolean`。注意，这个类可能是个从一个字符串转换而来的复杂类型。如果类型未知则该属性会被忽略|
|`description`|String|一个简短的组的描述，用于展示给用户。如果没有描述可用则该属性会被省略。推荐使用一个简短的段落描述，开头提供一个简要的总结，最后一行以句号（`.`）结束|
|`sourceType`|String|贡献property的来源类名。例如，如果property来自一个被`@ConfigurationProperties`注解的类，该属性将包括该类的全限定名。如果来源类型未知则该属性会被忽略|
|`defaultValue`|Object|当property没有定义时使用的默认值。如果property类型是个数组则该属性也可以是个数组。如果默认值未知则该属性会被忽略|
|`deprecated`|Deprecation|指定该property是否弃用。如果该字段没有弃用或该信息未知则该属性会被忽略。更多细节请查看下面|

每一个`properties`元素的`deprecation`属性包含的JSON对象可以包含如下的属性：

|名称|类型|目的|
|----|:----|:----|
|`level`|String|弃用的级别，可以是`warning`（默认）或者`error`。当一个属性有`warning`弃用级别，它应当还是会被绑定在环境里。但是，当它有一个`error`启用级别，这个属性就不再被管理，也不再被绑定。
|`reason`|String|对这个属性被弃用的原因的简短描述。没有原因则可能会被省略。推荐使用一个简短的段落描述，开头提供一个简要的总结，最后一行以句号（`.`）结束|
|`replacement`|String|属性的全名，代替弃用的属性。如果没有代替的属性则会被省略|

**注** 在Spring Boot 1.3之前，单个的`deprecated`布尔属性可以用来代替`deprecation`元素。在弃用的方式里，这仍旧被支持，但是不应当再被使用。如果没有可用的reason和replacement，一个空的`deprecation`对象应当被设置。

Deprecation也可以通过在暴露deprecated属性的getter方法上，添加`@DeprecatedConfigurationProperty`标注的方式，在代码中声明式地指定。比如，让我们假设`app.foo.target`属性令人困惑，被重命名成了`app.foo.name`：
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
**注** 没有办法设置`level`，因为代码还在处理这个属性，所以一直是`warning`。

上面的代码确保了弃用的属性依旧工作（在幕后委托给`name`属性）。一旦`getTarget`和`setTarget`方法可以从你的公共API移除，元数据里的自动的弃用提示也会一同消失。如果你想要保持提示，用`error`弃用级别添加手工的元数据，保证用户仍旧会收到关于那个属性的通知。当提供了`replacement`的时候，这会特别有用。