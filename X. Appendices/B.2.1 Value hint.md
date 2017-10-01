### 附录B.2.1 Value hint

The name attribute of each hint refers to the name of a property. In the initial example above, we provide 5 values for the spring.jpa.hibernate.ddl-auto property: none, validate, update, create and create-drop. Each value may have a description as well.

If your property is of type Map, you can provide hints for both the keys and the values (but not for the map itself). The special .keys and .values suffixes must be used to refer to the keys and the values respectively.

Let’s assume a foo.contexts that maps magic String values to an integer:

@ConfigurationProperties("foo")
public class FooProperties {

    private Map<String,Integer> contexts;
    // getters and setters
}
The magic values are foo and bar for instance. In order to offer additional content assistance for the keys, you could add the following to the manual meta-data of the module:

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
[Note]
Of course, you should have an Enum for those two values instead. This is by far the most effective approach to auto-completion if your IDE supports it.



