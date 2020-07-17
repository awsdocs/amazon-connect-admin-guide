# Contact block: Transfer to phone number<a name="transfer-to-phone-number"></a>

## Contact flow types<a name="transfer-to-phone-number-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Description<a name="transfer-to-phone-number-description"></a>
+ Transfers the customer to a phone number external to your instance\.
+ If this block is triggered during a chat conversation, the contact is routed down the **Error** branch\.

## Properties<a name="transfer-to-phone-number-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-phone-number-properties.png)

Note the following properties:
+ **Resume contact flow after disconnect**: This works only if the external party disconnects, and the customer doesn't disconnect\. \(If the customer disconnects, the whole call disconnects\.\)
+ **Send DTMF**: This property is useful to bypass some of the DTMF of the external party\. For example, if you know you'll need to press 1, 1, 362 to reach the external party, you can enter that here\.
+ **Caller ID number**: You can choose a number from your instance to appear as the caller ID\. This is useful in cases where you want to use a number that's different from the one the contact flow is actually using to make the call\.
+ **Caller ID name**: You can set a caller ID name, but there's no guarantee it will appear correctly to the customer\. For more information, see [Why your caller ID might not appear correctly to customers](queues-callerid.md#why-callerid-name-might-not-appear-correctly)\.

## Configuration tips<a name="transfer-to-phone-number-tips"></a>
+ [Submit a service quota increase request](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect) requesting that your business be allowed to make outbound calls to the country you specified\. If your business is not on the allow list for making the call, it will fail\. For more information, see [Countries you can call](amazon-connect-service-limits.md#country-code-allow-list)\.
+ If the country you want to select is not listed, you can submit a request to add countries you want to transfer calls to using the [Amazon Connect service quotas increase form](https://console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase&limitType=service-code-connect)\.
+ You can choose to end the contact flow when the call is transferred, or choose to **Resume contact flow after disconnect**, which returns the caller to your instance and resumes the contact flow after the transferred call ends\.

## Configured block<a name="transfer-to-phone-number-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/transfer-to-phone-number-configured.png)

## Scenarios<a name="transfer-to-phone-number-scenarios"></a>

See these topics for scenarios that use this block:
+ [Set up contact transfers](transfer.md)
+ [Set up outbound caller ID](queues-callerid.md)