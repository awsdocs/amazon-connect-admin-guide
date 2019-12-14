# Best Practices for Amazon Connect<a name="best-practices"></a>

This list of best practices can help you get the maximum benefit from Amazon Connect\. These best practices are for contact flows, user access and security, Lambda, chat, Amazon Lex, and the Contact Control Panel \(CCP\)\.

## Contact Flows<a name="bp-contact-flows"></a>
+ Use consistent attribute naming conventions across all AWS services\. Use camel case for yourAttributeNames to avoid confusion when passing and referencing variables\. 
+ Use standard naming conventions for attribute names\. Don't use spaces or special characters that could impact downstream reporting processes such as AWS Glue crawlers\. 
+ Create modular contact flows\. Make the flows as small as possible, and then combine modular flows into an end\-to\-end contact experience\. This helps to keep your flows manageable, and you won't require numerous regression testing cycles\.
+ Ensure all error branches are routed to a block that effectively handles the error or terminates the contact\.
+ Use a **Set logging behavior** block to enable or disable logging for segments of the contact flow where sensitive information is collected and can't be stored in CloudWatch\.
+ Use **Set recording behavior** block in your contact flow to disable and enable recordings according to your use case\. Keep in mind that Amazon Connect records conversations with agents only\. It doesn't record IVR interactions\.
+ Ensure that attributes used in the flow are set and referenced correctly\. If there are periods prepended to the attribute names, you are likely using JSONPath \($\.\) format while also selecting a variable type from the pick list\. For example:, using:
  + **Save text as attribute** and value `$.External.variableName` works as expected\.
  + `Use attribute` and value `variableName` works as expected\.
  + **Use attribute** and `$.External.varableName` results in a prepended period\. 
+ Before transferring a call to agent and putting that call in a queue, ensure that **Check hours of operation** and **Check staffing** blocks are used\. They verify that the call is within working hours and that agents are staffed to service\.
+ Ensure that callbacks are offered before and after queue transfer by using **Check queue status** blocks\. Include a condition for **Queue capacity** that is greater than X, where X is a number representing your expected queue capacity\.
  + If queue capacity exceeds the expected capacity, use a **Get Customer Input** block to offer a callback\. This retains the caller's position in the queue and calls them back when an agent is available\.
  + In the **Set callback number** block, choose the number to be used to call the customer back in the CCP\. Use **System** and **Customer Number** or a new number, collected by a **Store Customer Input** block, using **System** and **Stored customer input**\.
  + Finally, add a **Transfer to queue** block\. Configure it to **Transfer to callback queue** and configure the callback options to fit your specific use case\.
+ Use a **Loop prompts** block in your Customer queue flow to interrupt with a queued callback and external transfer option at regular intervals\. 
+ Ensure that all countries referenced in external transfers or used for outbound dialing are added to the service quota for your account/instance\.
+ Ensure that all numbers referenced in external transfers are in E\.164 format\. Drop the national trunk prefix that you use when calling locally\. This prefix would be the leading 0 for most of Europe, 1 for the US\. The prefix is replaced by the country code\. For example, the UK mobile number **07911 123456** in E\.164 format is **\+44 7911 123456 \(tel:\+447911123456\)**\.
+ Ensure that there are no infinite loops in the contact flow logic\. Also ensure that for each call, the contact flow connects the caller to an agent, bot, or transferred externally for further assistance\.

## User Access and Security Profiles<a name="bp-security-profiles"></a>
+ Ensure that all profile permissions are as restrictive as possible\. Allow access to only those resources absolutely required for the user's role\. For example, don't give agents permissions to create, read, or update users in Amazon Connect\.
+ Ensure that multi\-factor authentication \(MFA\) is set up through your SAML 2\.0 identity provider, or Radius server, if that's more applicable for your use case\. After MFA is set up, a third text box becomes visible on the Amazon Connect login page to provide the second factor\.
+ If you use an existing directory through AWS Directory Service or SAML\-based authentication for identity management, ensure that you follow all security requirements appropriate for your use case\. 
+ Use the **Login as administrator** button on the instance page of the AWS console only in emergency scenarios\. For example, use this option if you can't otherwise access the system because no administrator credentials or accounts with administrator permissions are available\. Do not use the administrator login to manage your contact center\.

## Lambda<a name="bp-lambda"></a>
+ Amazon Connect limits the duration of a sequence of Lambda functions to 20 seconds\. It times out with an error message when the total execution time exceeds this threshold\. Because customers hear silence while a Lambda function runs, we recommend adding a **Play prompt** block between functions to keep them engaged during the long interaction\. 

  By breaking up a chain of Lambda functions with the **Play prompt** block, you can invoke multiple functions that last longer than the 20 second threshold\.

## Chat and Amazon Lex<a name="bp-lex-bot-chat"></a>
+ You can use the same bot for both the voice and chat channels\. However, you may want the bot to respond differently based on the channel\. For example, you want to return SSML for voice so a number is read as a phone number, but you want to return normal text to chat\. You can do this by passing the **Channel** attribute\. For instructions, see [How to Use the Same Bot for Voice and Chat](one-bot-voice-chat.md)\. 
+ For voice, some words are best spelled phonetically to get the correct pronunciation, such as last names\. If this is the case with your scenario, include it in the design of your bot\. Or, you can keep the voice and chat bots separate\. 
+ Tell agents about the bot\. When a contact is connected to the agent, the agent sees the entire transcript in their window\. The transcript includes text from both the customer and the bot\.

## Contact Control Panel<a name="bp-ccp"></a>
+ If your agents use Google Chrome 71 to Chrome 75, and they use chat, add the CCP URL to the allow list in the agent's Chrome settings\. Otherwise, they won't hear the audio indicator notifying them that there's an incoming chat\. 

  For instructions, see this [Google Chrome Help article](https://support.google.com/chrome/answer/114662)\.