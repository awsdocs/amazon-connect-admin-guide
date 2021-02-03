# Contact flow logs stored in an Amazon CloudWatch log group<a name="contact-flow-logs-stored-in-cloudwatch"></a>

Contact flow logs are stored in an Amazon CloudWatch log group, in the same region as your Amazon Connect instance\. This log group is created automatically when [Enable contact flow logging](contact-flow-logs.md#enable-contact-flow-logs) is turned on for your instance\.

For example, the following image shows the CloudWatch log groups for two test instances\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cloudwatch-log-group.png)

 A log entry added as each block in your contact flow is triggered\. You can configure CloudWatch to send alerts when unexpected events occur during active contact flows\. 

**What happens if my log group is deleted?** You need to manually re\-create the CloudWatch log group\. Otherwise, Amazon Connect won't publish more logs\. 

## Pricing for contact flow logging<a name="pricing-contact-flow-logs"></a>

You are not charged for generating contact flow logs, but you are charged for using CloudWatch for generating and storing the logs\. Free tier customers are charged only for usage that exceeds service quotas\. For details about Amazon CloudWatch pricing, see [Amazon CloudWatch Pricing](https://aws.amazon.com/cloudwatch/pricing/)\.