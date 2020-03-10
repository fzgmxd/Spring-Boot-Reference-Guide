### 附录B.1.3. Hint属性

`hints`数组中包含的JSON对象能够包含以下属性：

|名称|类型|目的|
|----|:----|:----|
|`name`|String|该hint参考的property的全名。格式为小写句点分割的形式（比如`server.servlet.path`）。如果这个属性参考一个map（比如`system.contexts`），hint要么应用到map的key（`system.context.keys`）上，要么应用到value上（`system.context.values`）。该属性是强制性的|
|`values`|ValueHint[]|由`ValueHint`对象定义的有效值的列表（在下表中说明）。每一个入口都定义了值，并可能有一段描述|
|`providers`|ValueProvider[]|由`ValueProvider`对象定义的提供者的列表（本文档稍后将对此进行描述）。每一个入口都定义了提供者的名字和它的参数，如果有的话|

每一个`hint`元素的`values`属性包含的JSON对象可以包含如下的属性：

|名称|类型|目的|
|----|:----|:----|
|`value`|Object|该hint参考的元素的有效值。如果属性的类型是数组，那么也可以是有效值的数组。该属性是强制性的|
|`description`|String|一个简短的对有效值的描述，用于展示给用户。如果没有描述可用则该属性会被省略。推荐使用一个简短的段落描述，开头提供一个简要的总结，最后一行以句号（`.`）结束|

每一个`hint`元素的`providers`属性包含的JSON对象可以包含如下的属性：

|名称|类型|目的|
|----|:----|:----|
|`name`|String|提供者的名字，为该hint参考的元素提供额外的内容。|
|`parameters`|JSON object|提供者支持的任何额外的内容（更多细节，请查看提供者的文档）|
