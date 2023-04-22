# Schedule Adherence<a name="schedule-adherence"></a>

Contact center supervisors or managers track schedule adherence to understand when agents are following the schedule that you have created\. This helps ensure you achieve your service level targets, while improving agent productivity and customer satisfaction\.

Amazon Connect begins generating schedule adherence automatically as soon as a published schedule starts that has shift activities where `Adherence = yes`\. 

You can view Schedule Adherence metrics on the **Historical metrics** and **Real\-Time metrics** pages\. The Schedule Adherence metrics are: 
+ Adherent time
+ Adherence
+ Schedule time
+ Non\-adherent time\.

The following image shows an example of choosing Schedule Adherence metrics to appear in a historical metrics report\.

![\[The historical metrics page for agents, the table settings box, the schedule adherence metrics.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-schedule-adherence-metrics.png)

**Getting started:**

1. Schedule Adherence requires that schedules are created and published\. For more information, see  [Scheduling in Amazon Connect](scheduling.md)\.

1. Ensure you have the right permissions to access metrics and scheduling information\. For more information on the required permissions, see [ security profile permissions for forecasting, capacity planning, and scheduling](https://docs.aws.amazon.com/connect/latest/adminguide/required-optimization-permissions.html)\. 