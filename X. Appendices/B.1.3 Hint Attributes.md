### 附录B.1.3. 提示属性

The JSON object contained in the hints array can contain the following attributes:

Name	Type	Purpose
name

String

The full name of the property that this hint refers to. Names are in lowercase dashed form (e.g. server.servlet.path). If the property refers to a map (e.g. system.contexts) the hint either applies to the keys of the map (system.context.keys) or the values (system.context.values). This attribute is mandatory.

values

ValueHint[]

A list of valid values as defined by the ValueHint object (see below). Each entry defines the value and may have a description

providers

ValueProvider[]

A list of providers as defined by the ValueProvider object (see below). Each entry defines the name of the provider and its parameters, if any.

The JSON object contained in the values attribute of each hint element can contain the following attributes:

Name	Type	Purpose
value

Object

A valid value for the element to which the hint refers to. Can also be an array of value(s) if the type of the property is an array. This attribute is mandatory.

description

String

A short description of the value that can be displayed to users. May be omitted if no description is available. It is recommended that descriptions are a short paragraphs, with the first line providing a concise summary. The last line in the description should end with a period (.).

The JSON object contained in the providers attribute of each hint element can contain the following attributes:

Name	Type	Purpose
name

String

The name of the provider to use to offer additional content assistance for the element to which the hint refers to.

parameters

JSON object

Any additional parameter that the provider supports (check the documentation of the provider for more details).
