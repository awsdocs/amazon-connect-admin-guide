# Lambda functions and attributes<a name="attribs-with-lambda"></a>

Retrieve data from a system your organization uses internally, such as an ordering system or other database with a Lambda function, and store the values as attributes that can then be referenced in a flow\.

When the Lambda function returns a response from your internal system, the response is key\-value pairs of data\. You can reference the values returned in the External namespace, for example $\.External\.attributeName\. To use the attributes later in a flow, you can copy the key\-value pairs to user\-defined attributes using a **Set contact attributes** block\. You can then define logic to branch your contact based on attribute values by using a **Check contact attributes** block\. Any contact attribute retrieved from a Lambda function is overwritten with the next invocation of a Lambda function\. Make sure you store external attributes if you want to reference them later in a flow\.

**To store an external value from a Lambda function as a contact attribute**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing flow, or create a new one\.

1. Add an **Invoke AWS Lambda function** block, then choose the title of the block to open the settings for the block\.

1. Add the **Function ARN** to your AWS Lambda function that retrieves customer data from your internal system\.

1. After the **Invoke AWS Lambda function** block, add a **Set contact attributes** block and connect the **Success** branch of the **Invoke AWS Lambda function** block to it\.

1. Edit the **Set contact attributes** block, and select **Use attribute**\.

1. For **Destination key**, type a name to use as a reference to the attribute, such as customerName\. This is the value you use in the **Attribute** field in other blocks to reference this attribute\.

1. For **Type**, choose **External**\.

1. For **Attribute**, enter the name of the attribute returned from the Lambda function\. The name of the attribute returned from the function will vary depending on your internal system and the function you use\.

After this block executes during a flow, the value is saved as a user\-defined attribute with the name specified by the **Destination key**, in this case customerName\. It can be accessed in any block that uses dynamic attributes\.

To branch your flow based on the value of an external attribute, such as an account number, use a **Check contact attributes** block, and then add a condition to compare the value of the attribute to\. Next, branch the flow based on the condition\.

****

1. In the **Check contact attributes** block, for **Attribute to check** do one of the following:
   + Select **External** for the **Type**, then enter the key name returned from the Lambda function in the **Attribute** field\.
**Important**  
Any attribute returned from an AWS Lambda function is overwritten with the next function invocation\. To reference them later in a flow, store them as user\-defined attributes\.
   + Select **User Defined** for the **Type**, and in the **Attribute** field, type the name that you specified as the **Destination key** in the **Set contact attributes** block\.

1. Choose **Add another condition**\.

1. Under **Conditions to check**, choose the operator for the condition, then enter a value to compare to the attribute value\. A branch is created for each comparison you enter, letting you route the contact based on the conditions specified\. If no condition is matched, the contact takes the **No Match** branch from the block\.