# Create a Contact Lens rule that generates an EventBridge event<a name="contact-lens-rules-eventbridge-event"></a>

In real\-time or post\-call, you can get events and use them to trigger subsequent notifications or alerts, or aggregate reports outside of Amazon Connect\. There's a lot you can do with this data\. For example: 
+ Get real\-time alerts in a QuickSight dashboard\.
+ Create aggregated reported outside of Amazon Connect\.
+ Join data with your CRM\.
+ Connect your notification solution to EventBridge and make sure that by end of day, all of a certain type of events go to a certain inbox\. The payload tells you the contact, agent, and queue\. 

**To create a rule that generates an EventBridge event**

1. When you create your rule, choose **Generate EventBridge event** for the action\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-events-example1.png)

1. For **Action name**, enter the name for the event payload\.
**Note**  
The value you assign for **Action name** is visible in the EventBridge payload\. When you aggregate events, the action name provides an additional dimension that you can use to process them\. For example, you have 200 category names, but only 50 have a specific action name, such as NOTIFY\_CUSTOMER\_RETENTION\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-add-eb-action.png)

1. Choose **Next**\. Review and then **Save**\.

1. After you add rules, they are applied to new contacts that occur after the rule was added\. Rules are applied when Contact Lens analyzes conversations\.

   You cannot apply rules to past, stored conversations\. 

1. To leverage the EventBridge data, subscribe to the EventBridge event type\. See the next procedure\.

## Subscribe to EventBridge event types<a name="subscribe-eb-eventtype"></a>

To subscribe to EventBridge event types, create a custom EventBridge rule that matches the following:
+ "source" = "aws\.connect"
+ "detail\-type" = "Contact Lens Analysis State Change" \(or **Contact Lens Post Call Rules Matched** or **Contact Lens Realtime Rules Matched**\)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-eb-rules-events.png)

### Example EventBridge payloads<a name="eb-payload"></a>

Following is an example of what the EventBridge payload looks like when **Contact Lens Post Call Rules Matched**\. 

```
{
 "version": "0", // set by EventBridge
 "id": "aaaaaaaa-bbbb-cccc-dddd-bf3703467718", // set by EventBridge
 "source": "aws.connect",
 "detail-type": "Contact Lens Post Call Rules Matched", 
 "account": "your AWS account ID",
 "time": "2020-04-27T18:43:48Z",
 "region": "us-east-1", // set by EventBridge
 "resources": ["arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN"],
 "detail": {
    "version": "1.0",
    "ruleName": "ACCOUNT_CANCELLATION", // Rule name
    "actionName": "NOTIFY_CUSTOMER_RETENTION",  
    "instanceArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN",
    "contactArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN/contact/contact-ARN",
    "agentArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN/agent/agent-ARN",
    "queueArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN/queue/queue-ARN",
    }
}
```

Following is an example of what the payload looks like when **Contact Lens Realtime Rules Matched**\. 

```
{
 "version": "0", // set by EventBridge
 "id": "aaaaaaaa-bbbb-cccc-dddd-bf3703467718", // set by EventBridge
 "source": "aws.connect",
 "detail-type": "Contact Lens Realtime Rules Matched", 
 "account": "your AWS account ID",
 "time": "2020-04-27T18:43:48Z",
 "region": "us-east-1", // set by EventBridge
 "resources": ["arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN"],
 "detail": {
     "version": "1.0",
     "ruleName": "ACCOUNT_CANCELLATION", // Rule name
     "actionName": "NOTIFY_CUSTOMER_RETENTION",
      "instanceArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN",
     "contactArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN/contact/contact-ARN",
     "agentArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN/agent/agent-ARN",
     "queueArn": "arn:aws:connect:us-east-1:your AWS account ID:instance/instance-ARN/queue/queue-ARN",
      }
}
```