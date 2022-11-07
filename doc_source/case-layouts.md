# Case layouts<a name="case-layouts"></a>

This topic is intended for developers who are using the Amazon Connect Cases APIs\.

There is an underlying resource called a *case layout* that is linked to the case template\. Technically, it is the case layout that holds the display elements for a case, such as: 
+ Which fields to display\.
+ The section, either Top panel or More information\.
+ The order within a section to display these fields

Whereas it's the case template that mandates a particular schema, such as required case fields\. 

 The case layout is linked to a case template\. 

**Note**  
You can create a case template and not link it to a case layout\. Any case created with a case template that is not linked to a case layout will display system fields in a default order\. 