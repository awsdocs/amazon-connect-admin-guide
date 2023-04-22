# Search flow logs<a name="search-contact-flow-logs"></a>

Before you can search flow logs, you must first [enable flow logging](contact-flow-logs.md)\. 

Logs will be created for conversations that occur after logging is enabled\.

**To search flow logs**

1. Open Amazon CloudWatch console, go to **Logs**, **Log groups**\. The following image shows a sample log group named **mytest88**\.  
![\[The Amazon CloudWatch console, log groups section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cloudwatch-log-group.png)

1. Choose the log group for your instance\.

   A list of log streams will be displayed\.

1. To search all the log streams in the instance, choose **Search log group**, as shown in the following image\.  
![\[The search log group button on the /aws/connect/mytest88 page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-flow-logs-choose-search.png)

1. In the search box, enter the string you want to search for, for example, all or a portion of the contact ID\. 

1. After a couple of moments \(longer depending on how big your log is\), Amazon CloudWatch returns results\. The following image shows a sample contact ID **fb3304c2**, and the result\.  
![\[The log events listed for mytest88.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-flow-logs-search-results.png)

1. You can open each event to see what happened\. The following image shows the event for when a **Play prompt** block runs in a flow\.  
![\[The event for a Play prompt block.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-flow-logs-example-event.png)