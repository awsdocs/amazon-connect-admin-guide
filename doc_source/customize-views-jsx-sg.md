# Customize views<a name="customize-views-jsx-sg"></a>

You can customize the look and feel of the layouts of View resources by leveraging HTML or JSX when you pass in input parameters to the show view block\.

As a simple example, create a flow with one show view block and select the **Details view**\. In the **Sections** field use the below JSON to see how either HTML or JSX expressions get processed\.

**HTML example**

```
{
"TemplateString": 
     "<TextContent>Steps:<ol><li>Customer provides incident information</li><li>Customer provides receipts and agrees with 
         amount</li> <li>Customer receives reimbursement</li></ol></TextContent>"
}
```

**JSX example**

```
{
 "TemplateString":
"Please provide an introduction to the customers. Ask them how their day is going
Things to say:
Hello, how are you today? My name is Bob, who am I speaking to?"
}
```