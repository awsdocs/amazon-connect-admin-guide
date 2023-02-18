# Error notifications: When Amazon Connect Rules action fails to run<a name="error-notifications-rule-fails-to-run"></a>

It's important to know when a specific rule action has failed in a production environment, and what caused the failure\. Then you can proactively mitigate such failures in future\.

To get real\-time insights on the actions that failed to run, you integrate Amazon Connect Rules with Amazon EventBridge events\. This enables you to be notified when, for example, the "Create task" action failed to run because the maximum number of **Concurrent active tasks per instance** reached the service quota\. When this happens, Amazon Connect sends error notifications using Amazon EventBridge events\.

Events are emitted on a [best effort](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-service-event.html) basis\.

## Subscribe to EventBridge notifications<a name="rule-error-notifications-subscribe"></a>

To subscribe to these notifications, create a custom EventBridge rule that matches the following:
+ "source" = "aws\.connect"
+ "detail\-type" = "Contact Lens Rules Action Execution Failed"

You can also add to the pattern to be notified when a specific event code occurs\. For more information, see [Event Patterns](https://docs.aws.amazon.com/eventbridge/latest/userguide/filtering-examples-structure.html) in the *Amazon EventBridge User Guide*\.

The format of a notification looks like the following sample: 

```
{
  "version": "0",
  "id": "8d122163-6c07-f8cb-06e7-373a1bcf8fc6",
  "source": "aws.connect",
  "detail-type": "Amazon Connect Rules Action Execution Failed",
  "account": "123456789012",
  "time": "2022-01-05T01:30:42Z",
  "region": "us-east-1",
  "resources": ["arn:aws:connect:us-east-1:123456789012:instance/cb54730f-5aac-4376-b2f4-7c822889931e"],
  "detail": {
    "ruleId": "7410c94b-21c2-4db0-a707-c6d751edbe8f",
    "actionType": "CREATE_TASK",
    "triggerEvent": "THIRD_PARTY",
    "instanceArn": "arn:aws:connect:us-east-1:123456789012:instance/cb54730f-5aac-4376-b2f4-7c822889931e",
    "reasonCode": "ResourceNotFoundException",
    "error": "ContactFlowId provided does not belong to connect instance",
    "additionalInfo": "{\n  \"message\": \"Not Found\",\n  \"code\": \"ResourceNotFoundException\",\n  \"statusCode\": 404,\n  \"time\": \"2022-01-03T20:23:07.073Z\",\n  \"requestId\": \"048e4403-71c1-47d6-96fc-825744f518e7\",\n  \"retryable\": false,\n  \"retryDelay\": 28.217537834500316\n}"
  }
}
```

## Supported action types<a name="supported-action-types-rules"></a>
+ `CREATE_TASK`
+ `GENERATE_EVENTBRIDGE_EVENT`
+ `SEND_NOTIFICATION`

For information about `ASSIGN_CONTACT_CATEGORY`, see [Error notifications: When Contact Lens can't analyze a contact](contact-lens-error-notifications.md)\.

## Supported trigger events<a name="supported-trigger-events"></a>
+ `REAL_TIME_CALL`
+ `POST_CALL`
+ `POST_CHAT`
+ `THIRD_PARTY`

## Reason codes for failed actions<a name="reason-codes-failed-actions"></a>

When an action fails, the error notification service collects the reason codes from the supported actions\. For more information about the reason codes for Task and EventBridge action failures, see the following topics:
+ For reason codes for Task action failures, see [Errors](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartTaskContact.html#API_StartTaskContact_Errors) in the **StartTaskContact** API topic in the *Amazon Connect API Reference Guide*\.
+ For reason codes for EventBridge action failures, see [Errors](https://docs.aws.amazon.com/eventbridge/latest/APIReference/API_PutEvents.html#API_PutEvents_Errors) in the **PutEvents** API topic in the *Amazon EventBridge API Reference Guide*\.