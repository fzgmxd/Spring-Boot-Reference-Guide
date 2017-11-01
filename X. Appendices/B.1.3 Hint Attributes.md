### 附录B.1.3. 提示属性

`hints`数组中包含的JSON对象能够包含以下属性：

|名称|类型|目的|
|----|:----|:----|
|`name`|String|这个提示参考的property的全名。格式为小写虚线分割的形式（比如`server.servlet.path`）。如果这个属性参考一个map（比如`system.contexts`），提示要么应用到map的key（`system.context.keys`）上，要么应用到value上（`system.context.values`）。该属性是强制性的|
|`values`|ValueHint[]|由`ValueHint`对象定义的有效值的列表（看下面）。每一个入口都定义了值，并可能有一段描述|
|`providers`|ValueProvider[]|由`ValueProvider`对象定义的提供者的列表（看下面）。每一个入口都定义了提供者的名字和它的参数，如果有的话|

每一个`hint`元素的`values`属性包含的JSON对象可以包含如下的属性：

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
