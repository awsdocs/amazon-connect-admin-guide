# Sample Lambda Integration<a name="sample-lambda-integration"></a>

Type: Contact flow \(inbound\)

This contact flow shows you how to invoke a Lambda function and do a data dip, that is, retrieve information about the customer\. The data dip uses the caller's phone number to look up the US state they are calling from\. Here's how it works:

1. A prompt tells the caller that a data dip is being performed\. 

1. The Invoke Lambda function block triggers **state\-lookup**\. This sample Lambda function determines the location of the phone number\. The function times out in 4 seconds\. If it times out, it plays a prompt that says "Sorry, we failed to find the state for your phone number's area code\." 

1. In the **Check contact attributes** block, it checks the match conditions of **State**, which is an external attribute\. It uses an external contact attribute because it's getting data by using a process that's external to Amazon Connect

1. A prompt tells you that it's returning you back to **Sample inbound flow**, and then starts the **Transfer flow** block\. 

1. If the transfer fails, it plays a prompt and then disconnects the call\. 

For more information about using attributes, see [Using Attributes with a Lambda Function](use-attributes-cust-exp.md#attribs-with-lambda)\.