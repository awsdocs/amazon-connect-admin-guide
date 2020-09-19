# Parameter restrictions for actions in the Amazon Connect Flow language<a name="flow-language-actions-parameter-restrictions"></a>

There are several restrictions on parameters\. Here's what they mean:
+ Must be defined statically\. This means that JSONPath cannot be used at all in this value\.
+ Must be defined statically or as a single valid JSONPath identifier\. 

  If JSONPath is used, it must be the entirety of the value; you can't specify an input of "My name is $\.Name"\. Further, the JSONPath must be valid \- $\.Attributes\.stuff is okay, $\.BadValue is not okay because there's no "BadValue" path on the object used by flows\.
+ May be defined statically or dynamically\. Anything goes\. A value of "My name is $\.Name" is fine here, as well as a fully static value\.