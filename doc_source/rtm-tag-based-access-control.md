# Tag\-based access control<a name="rtm-tag-based-access-control"></a>

You can use resource tags and access control tags to apply granular access to users, queues, and routing profiles for real\-time metrics\. For example, you can control who has access to view specific users, queues, and routing profile real\-time metrics\. The following examples show the difference between real time metric reports with and without the use of tag based access controls\.

Without tag\-based access controls, you see all queues, routing profiles, and agents:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tag-based-access-control-metrics-without.png)

With tag\-based access controls, you see a limited set of queues, routing profiles, and agents:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tag-based-access-control-metrics-with.png)

Tag\-based access controls enable you to configure granular access to specific resources based on assigned resource tags\. You can configure tag based access controls via the API/SDK or within the Amazon Connect console \(for supported resources\)\. You must configure user resource tags and access control tags before tag\-based access control is applied to users for the agent activity audit report\. For more information, please see [Tagging Resources in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tagging.html) and [Tag\-based Access Control in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tag-based-access-control.html)\.

## How to enable tag\-based Access control for real\-time metrics<a name="rtm-tag-based-access-control-how-to-enable"></a>

To use tags to control access to users, queues, and routing profiles for real\-time metrics, you must first configure resource tags and access control tags\. For more information, please see [Tagging Resources in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tagging.html) and [Tag\-based Access Control in Amazon Connect](https://docs.aws.amazon.com/connect/latest/adminguide/tag-based-access-control.html)\.

After your resource tags and access control tags are configured, you must apply the appropriate permissions\. When your resource tags, access control tags, and permissions have been appropriately configured, you will have access controls applied to users, queues, and routing profiles for real\-time metrics\.

## Permissions<a name="rtm-tag-based-access-control-permissions"></a>

To view real\-time metrics reports with tag\-based access controls applied, you need to be assigned to a security profile that has Access selected for **Real\-time metrics** or has Access selected for **Access metrics** permission, along with access to the resources\. Note that if you enable **Access metrics**, then **Real\-time metrics, Historical Metrics**, and **Agent Activity Audit** will be filled in automatically, and you will be enabling users to see all data for historical metrics for which tag\-based access controls are not currently applied\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-tag-based-access-control-perm.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-tag-based-access-control-perm-2.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-tag-based-access-control-perm-3.png)

## Functionality limitations<a name="rtm-tag-based-access-control-limitations"></a>

The following limitations apply to tag\-based access controls for real\-time metrics\.

1. You can only filter and group tables by the primary resource \(user, queue, or routing profile\)\. You cannot filter and group tables by non\-primary resources\. For example, you cannot filter by queue in an agent table and you cannot group by queue in a routing profile table\.

1. Drill\-down button disabled within tables except for **View queue graphs**\. For example, you cannot choose **View agents** in a queue table\.

1. Access to the homepage service level dashboard is disabled\.

1. Access to view **Agent Queues** is disabled\.

1. **Agent Adherence** table is not yet supported\.

## Transitioning to tag\-based access control<a name="rtm-tag-based-access-control-transitioning"></a>

If you open a saved report containing tables with users, queues, or routing profiles that you don’t have access to anymore due to tag\-based access control, or if groupings or non\-primary filters are applied to tables, you won’t see data in those tables\. To fix, you can edit your table filters for agents, queues, or routing profiles that you have access to, create a new report with resources you have access to, or remove the groupings and non\-primary filters from the table\.