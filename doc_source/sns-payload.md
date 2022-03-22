# Amazon SNS payload used in message streaming<a name="sns-payload"></a>

After you’ve enabled message streaming successfully, you may need to filter the message to send it to the intended participant: agent, customer, or all\.

To filter by participant, read the specific SNS headers attribute— `MessageVisibility`—to determine whether the message is intended for customer\-only, agent\-only, or all\. 
+ To send to the customer only: For all code that faces the customer, clients need to filter out messages intended for the customer and build the following logic for forwarding the message to them\.

  ```
  if ( ( MessageVisibility == CUSTOMER || MessageVisibility == ALL)  && ParticipantRole != CUSTOMER )
  ```
+ To send to the agent only:

  ```
  if ( ( MessageVisibility == AGENT || MessageVisibility == ALL)  && ParticipantRole != AGENT )
  ```

You can also leverage the filtering capability in Amazon SNS by building custom [subscription filtering policies](https://docs.aws.amazon.com/sns/latest/dg/sns-subscription-filter-policies.html)\. This offloads the message filtering logic from the SNS topic subscriber to the SNS service itself\.

## Message attributes in the payload<a name="sns-message-attributes"></a>

Following is a description of each message attribute in the Amazon SNS payload:
+ `InitialContactId`: The initial contact ID of the chat\.
+ `ContactId`: The current contact ID of the chat\. The `InitialContactId` and `ContactId` can differ if there has been new agent in the chat or the queue\-to\-queue contact flow\.
+ `ParticipantRole`: The participant who sent the message\.
+ `InstanceId`: The Amazon Connect instance ID\.
+ `AccountId`: The AWS account ID\.
+ `Type`: Possible values: `EVENT`, `MESSAGE`\.
+ `ContentType`: Possible values: `application/vnd.amazonaws.connect.event.typing`, `application/vnd.amazonaws.connect.event.participant.joined`, `application/vnd.amazonaws.connect.event.participant.left`, `application/vnd.amazonaws.connect.event.transfer.succeeded`, `application/vnd.amazonaws.connect.event.transfer.failed`, `application/vnd.amazonaws.connect.message.interactive`, `application/vnd.amazonaws.connect.event.chat.ended`, and more\. 
+ `MessageVisibility`: Possible values: `AGENT`, `CUSTOMER`, `ALL`\.

## Example SNS payload<a name="sns-message-payload"></a>

```
{
  "Type" : "Notification",
  "MessageId" : "ccccccccc-cccc-cccc-cccc-ccccccccccccc",
  "TopicArn" : "arn:aws:sns:us-west-2:009969138378:connector-svc-test",
  "Message" :  "{\"AbsoluteTime\":\"2021-09-08T13:28:24.656Z\",\"Content\":\"help\",\"ContentType\":\"text/plain\",\"Id\":\"333333333-be0d-4a44-889d-d2a86fc06f0c\",\"Type\":\"MESSAGE\",\"ParticipantId\":\"bbbbbbbb-c562-4d95-b76c-dcbca8b4b5f7\",\"DisplayName\":\"Jane\",\"ParticipantRole\":\"CUSTOMER\",\"InitialContactId\":\"33333333-abc5-46db-9ad5-d772559ab556\",\"ContactId\":\"33333333-abc5-46db-9ad5-d772559ab556\"}",
  "Timestamp" : "2021-09-08T13:28:24.860Z",
  "SignatureVersion" : "1",
  "Signature" : "examplegggggg/1tEBYdiVDgJgBoJUniUFcArLFGfg5JCvpOr/v6LPCHiD7A0BWy8+ZOnGTmOjBMn80U9jSzYhKbHDbQHaNYTo9sRyQA31JtHHiIseQeMfTDpcaAXqfs8hdIXq4XZaJYqDFqosfbvh56VPh5QgmeHTltTc7eOZBUwnt/177eOTLTt2yB0ItMV3NAYuE1Tdxya1lLYZQUIMxETTVcRAZkDIu8TbRZC9a00q2RQVjXhDaU3k+tL+kk85syW/2ryjjkDYoUb+dyRGkqMy4aKA22UpfidOtdAZ/GGtXaXSKBqazZTEUuSEzt0duLtFntQiYJanU05gtDig==",
  "SigningCertURL" : "https://sns.us-west-2.amazonaws.com/SimpleNotificationService-11111111111111111111111111111111.pem",
  "UnsubscribeURL" : "https://sns.us-west-2.amazonaws.com/?Action=Unsubscribe&SubscriptionArn=arn:aws:sns:us-west-2:000000000000:connector-svc-test:22222222-aaaa-bbbb-cccc-333333333333",
  "MessageAttributes" : {
    "InitialContactId" : {"Type":"String","Value":"33333333-abc5-46db-9ad5-d772559ab556"},
    "MessageVisibility" : {"Type":"String","Value":"ALL"},
    "Type" : {"Type":"String","Value":"MESSAGE"},
    "AccountId" : {"Type":"String","Value":"999999999999"},
    "ContentType" : {"Type":"String","Value":"text/plain"},
    "InstanceId" : {"Type":"String","Value":"dddddddd-b64e-40c5-921b-109fd92499ae"},
    "ContactId" : {"Type":"String","Value":"33333333-abc5-46db-9ad5-d772559ab556"},
    "ParticipantRole" : {"Type":"String","Value":"CUSTOMER"}
  }
}
```