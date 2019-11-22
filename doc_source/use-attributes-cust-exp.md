# How to Use Contact Attributes to Personalize the Customer Experience<a name="use-attributes-cust-exp"></a>

Contact attributes in your contact flows can provide a more personalized customer experience\. For example, specify a custom flow based on comparing an attribute to a value\. You then route the contact based on the value comparison, such as routing customers to different tiers of support based on their account number\. Or retrieve a customer's name and save it as an attribute\. Include the name attribute in a text to speech string so that the customer's name is said during the interaction\.

**Tip**  
Contact attributes are shared across all contacts with the same InitialContactId\. This means that while carrying out transfers, for example, a contact attribute updated in the transfer flow updates the attribute's value in both CTR's contact attributes \(that is, the Inbound and Transfer contact attributes\)\. 

The steps in the following sections describe how to use contact attributes with different blocks in a contact flow\.

## Using a Set Contact Attributes Block<a name="use-set-contact-attrib-block"></a>

Use a **Set contact attributes** block to set a value that is later referenced in a contact flow\. For example, create a personalized greeting for customers routed to a queue based on the type of customer account\. You could also define an attribute for a company name or line of business to include in the text to speech strings said to a customer\. The **Set contact attributes** block is useful for copying attributes retrieved from external sources to user\-defined attributes\.

**To set a contact attribute with a Set contact attributes block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Set contact attributes** block\.

1. Edit the **Set contact attributes** block, and choose **Use text**\.

1. For the **Destination key**, provide a name for the attribute, such as *Company*\. This is the value you use for the **Attribute** field when using or referencing attributes in other blocks\. For the **Value**, use your company name\.

   You can also choose to use an existing attribute as the basis for creating the new attribute\.

## Capture Customer Input and Store it as an Attribute<a name="capture-cust-input"></a>

You can use an attribute to request a callback number from a customer, store the value of the attribute, and then reference the attribute in a **Set callback number** block to set the number to dial the customer\. You could also use a **Store customer input** block to capture any numeric input from a customer, such as an account or order number\.

**To create an attribute from customer input with a Store customer input block**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add a **Store customer input** block\.

1. Edit the block, and select **Text to speech \(Ad hoc\)**\.

1. In the **Enter text** box, type a message that is said to customers when they call, such as “Please enter your phone number\.”

1. In the **Customer input** section, select **Phone number**, and then choose the format\. **Local format** is for a number in the same country as the region in which you created your Amazon Connect instance\. **International format/Enforce E\.164** is for numbers to a country other than the country in which you created your instance\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/store-customer-input.png)

1. Add a **Set callback number** block to your contact flow, and connect it to the **Get customer input** block\.

1. Under **Use attributes**, for **Type**, choose **System**\. For **Attribute**, choose **Stored customer input**\. The callback number is set to the number the customer entered when asked to enter their phone number\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-callback-number.png)

## Using Attributes with a Lambda Function<a name="attribs-with-lambda"></a>

Retrieve data from a system your organization uses internally, such as an ordering system or other database with a Lambda function, and store the values as attributes that can then be referenced in a contact flow\.

When the Lambda function returns a response from your internal system, the response is key\-value pairs of data\. You can reference the values returned in the External namespace, for example $\.External\.attributeName\. To use the attributes later in a contact flow, you can copy the key\-value pairs to user\-defined attributes using a **Set contact attributes** block\. You can then define logic to branch your contact based on attribute values by using a **Check contact attributes** block\. Any contact attribute retrieved from a Lambda function is overwritten with the next invocation of a Lambda function\. Make sure you store external attributes if you want to reference them later in a contact flow\.

**To store an external value from a Lambda function as a contact attribute**

1. In Amazon Connect, choose **Routing**, **Contact flows**\.

1. Select an existing contact flow, or create a new one\.

1. Add an **Invoke AWS Lambda function** block, then choose the title of the block to open the settings for the block\.

1. Add the **Function ARN** to your AWS Lambda function that retrieves customer data from your internal system\.

1. After the **Invoke AWS Lambda function** block, add a **Set contact attributes** block and connect the **Success** branch of the **Invoke AWS Lambda function** block to it\.

1. Edit the **Set contact attributes** block, and select **Use attribute**\.

1. For **Destination key**, type a name to use as a reference to the attribute, such as customerName\. This is the value you use in the **Attribute** field in other blocks to reference this attribute\.

1. For the **Type**, choose **External**\.

1. For **Attribute** type the name of the attribute returned from the Lambda function\. The name of the attribute returned from the function will vary depending on your internal system and the function you use\.

After this block executes during a contact flow, the value is saved as a user\-defined attribute with the name specified by the **Destination key**, in this case customerName\. It can be accessed in any block that uses dynamic attributes\.

To branch your contact flow based on the value of an external attribute, such as an account number, use a **Check contact attributes** block, and then add a condition to compare the value of the attribute to\. Next, branch the contact flow based on the condition\.

****

1. In the **Check contact attributes** block, for **Attribute to check** do one of the following:
   + Select **External** for the **Type**, then enter the key name returned from the Lambda function in the **Attribute** field\.
**Important**  
Any attribute returned from an AWS Lambda function is overwritten with the next function invocation\. To reference them later in a contact flow, store them as user\-defined attributes\.
   + Select **User Defined** for the **Type**, and in the **Attribute** field, type the name that you specified as the **Destination key** in the **Set contact attributes** block\.

1. Choose **Add another condition**\.

1. Under **Conditions to check**, choose the operator for the condition, then enter a value to compare to the attribute value\. A branch is created for each comparison you enter, letting you route the contact based on the conditions specified\. If no condition is matched, the contact takes the **No Match** branch from the block\.

## "$" is a Special Character<a name="dollar-sign-special"></a>

Amazon Connect treats the "$" character as a special character\. You can't use it in a key when setting an attribute\. 

 For example, let's say you're creating an interact block with text\-to\-speech\. You set an attribute like this: 

 ` {"$one":"please read this text"} ` 

When Amazon Connect reads this text, it will read "dollar sign one" to the contact instead of "please read this text\." Also, if you were to include $ in a key and try to reference the value later using Amazon Connect, it won't retrieve the value\. 

Amazon Connect does log and pass the full key:value pair `({"_$one":"please read this text"})` to integrations such as Lambda\. 