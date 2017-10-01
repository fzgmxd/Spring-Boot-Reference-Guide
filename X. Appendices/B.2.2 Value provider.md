### 附录B.2.2 Value provider

Providers are a powerful way of attaching semantics to a property. We define in the section below the official providers that you can use for your own hints. Bare in mind however that your favorite IDE may implement some of these or none of them. It could eventually provide its own as well.

[Note]
As this is a new feature, IDE vendors will have to catch up with this new feature.
The table below summarizes the list of supported providers:

Name    Description
any

Permit any additional value to be provided.

class-reference

Auto-complete the classes available in the project. Usually constrained by a base class that is specified via the target parameter.

handle-as

Handle the property as if it was defined by the type defined via the mandatory target parameter.

logger-name

Auto-complete valid logger names. Typically, package and class names available in the current project can be auto-completed.

spring-bean-reference

Auto-complete the available bean names in the current project. Usually constrained by a base class that is specified via the target parameter.

spring-profile-name

Auto-complete the available Spring profile names in the project.

[Tip]
No more than one provider can be active for a given property but you can specify several providers if they can all manage the property in some ways. Make sure to place the most powerful provider first as the IDE must use the first one in the JSON section it can handle. If no provider for a given property is supported, no special content assistance is provided either.
Any

The any provider permits any additional values to be provided. Regular value validation based on the property type should be applied if this is supported.

This provider will be typically used if you have a list of values and any extra values are still to be considered as valid.

The example below offers on and off as auto-completion values for system.state; any other value is also allowed:

{"hints": [
    {
        "name": "system.state",
        "values": [
            {
                "value": "on"
            },
            {
                "value": "off"
            }
        ],
        "providers": [
            {
                "name": "any"
            }
        ]
    }
]}
Class reference

The class-reference provider auto-completes classes available in the project. This provider supports these parameters:

Parameter   Type    Default value   Description
target

String (Class)

none

The fully qualified name of the class that should be assignable to the chosen value. Typically used to filter out non candidate classes. Note that this information can be provided by the type itself by exposing a class with the appropriate upper bound.

concrete

boolean

true

Specify if only concrete classes are to be considered as valid candidates.

The meta-data snippet below corresponds to the standard server.servlet.jsp.class-name property that defines the JspServlet class name to use:

{"hints": [
    {
        "name": "server.servlet.jsp.class-name",
        "providers": [
            {
                "name": "class-reference",
                "parameters": {
                    "target": "javax.servlet.http.HttpServlet"
                }
            }
        ]
    }
]}
Handle As

The handle-as provider allows you to substitute the type of the property to a more high-level type. This typically happens when the property has a java.lang.String type because you don’t want your configuration classes to rely on classes that may not be on the classpath. This provider supports these parameters:

Parameter   Type    Default value   Description
target

String (Class)

none

The fully qualified name of the type to consider for the property. This parameter is mandatory.

The following types can be used:

Any java.lang.Enum that lists the possible values for the property (By all means, try to define the property with the Enum type instead as no further hint should be required for the IDE to auto-complete the values).
java.nio.charset.Charset: auto-completion of charset/encoding values (e.g. UTF-8)
java.util.Locale: auto-completion of locales (e.g. en_US)
org.springframework.util.MimeType: auto-completion of content type values (e.g. text/plain)
org.springframework.core.io.Resource: auto-completion of Spring’s Resource abstraction to refer to a file on the filesystem or on the classpath. (e.g. classpath:/foo.properties)
[Note]
If multiple values can be provided, use a Collection or Array type to teach the IDE about it.
The meta-data snippet below corresponds to the standard liquibase.change-log property that defines the path to the changelog to use. It is actually used internally as a org.springframework.core.io.Resource but cannot be exposed as such as we need to keep the original String value to pass it to the Liquibase API.

{"hints": [
    {
        "name": "liquibase.change-log",
        "providers": [
            {
                "name": "handle-as",
                "parameters": {
                    "target": "org.springframework.core.io.Resource"
                }
            }
        ]
    }
]}
Logger name

The logger-name provider auto-completes valid logger names. Typically, package and class names available in the current project can be auto-completed. Specific frameworks may have extra magic logger names that could be supported as well.

Since a logger name can be any arbitrary name, really, this provider should allow any value but could highlight valid packages and class names that are not available in the project’s classpath.

The meta-data snippet below corresponds to the standard logging.level property, keys are logger names and values correspond to the standard log levels or any custom level:

{"hints": [
    {
        "name": "logging.level.keys",
        "values": [
            {
                "value": "root",
                "description": "Root logger used to assign the default logging level."
            }
        ],
        "providers": [
            {
                "name": "logger-name"
            }
        ]
    },
    {
        "name": "logging.level.values",
        "values": [
            {
                "value": "trace"
            },
            {
                "value": "debug"
            },
            {
                "value": "info"
            },
            {
                "value": "warn"
            },
            {
                "value": "error"
            },
            {
                "value": "fatal"
            },
            {
                "value": "off"
            }

        ],
        "providers": [
            {
                "name": "any"
            }
        ]
    }
]}
Spring bean reference

The spring-bean-reference provider auto-completes the beans that are defined in the configuration of the current project. This provider supports these parameters:

Parameter   Type    Default value   Description
target

String (Class)

none

The fully qualified name of the bean class that should be assignable to the candidate. Typically used to filter out non candidate beans.

The meta-data snippet below corresponds to the standard spring.jmx.server property that defines the name of the MBeanServer bean to use:

{"hints": [
    {
        "name": "spring.jmx.server",
        "providers": [
            {
                "name": "spring-bean-reference",
                "parameters": {
                    "target": "javax.management.MBeanServer"
                }
            }
        ]
    }
]}
[Note]
The binder is not aware of the meta-data so if you provide that hint, you will still need to transform the bean name into an actual Bean reference using the ApplicationContext.
Spring profile name

The spring-profile-name provider auto-completes the Spring profiles that are defined in the configuration of the current project.

The meta-data snippet below corresponds to the standard spring.profiles.active property that defines the name of the Spring profile(s) to enable:

{"hints": [
    {
        "name": "spring.profiles.active",
        "providers": [
            {
                "name": "spring-profile-name"
            }
        ]
    }
]}


