# Real\-time metrics tag\-based access control<a name="rtm-tag-based-access-control"></a>

You can use resource tags and access control tags to apply granular access to users, queues, and routing profiles for real\-time metrics\. For example, you can control who has access to view specific users, queues, and routing profiles on the **Real\-time metrics** page\. 

Without tag\-based access controls, all queues, routing profiles, and agents appear on the **Real\-time metrics** page, as shown in the following image\.

![\[The real-time metrics page showing all resources.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tag-based-access-control-metrics-without.png)

With tag\-based access controls, a limited set of queues, routing profiles, and agents appear on the **Real\-time metrics** page, as shown in the following image\.

![\[The real-time metrics page showing a limited set of resources.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tag-based-access-control-metrics-with.png)

Tag\-based access controls enable you to configure granular access to specific resources based on assigned resource tags\. You can configure tag based access controls by using the API/SDK or within the Amazon Connect console \(for supported resources\)\. You must configure user resource tags and access control tags before tag\-based access control is applied to users for the agent activity audit report\. For more information, see [Tagging resources in Amazon Connect](tagging.md) and [Tag\-based access control](tag-based-access-control.md)\. 

## How to enable tag\-based access control for real\-time metrics<a name="rtm-tag-based-access-control-how-to-enable"></a>

To use tags to control access to users, queues, and routing profiles for real\-time metrics, you must first configure resource tags and access control tags\. For more information, see [Tagging resources in Amazon Connect](tagging.md) and [Tag\-based access control](tag-based-access-control.md)

After your resource tags and access control tags are configured, you must apply the appropriate permissions\. When your resource tags, access control tags, and permissions have been appropriately configured, you will have access controls applied to users, queues, and routing profiles for real\-time metrics\.

## Permissions<a name="rtm-tag-based-access-control-permissions"></a>

To view real\-time metrics reports that have tag\-based access controls applied to them, you need to be assigned to a security profile that has permissions to: 
+ Access metrics\.
+ Access the resources you want to view, such as routing profiles and queues\.

### Permissions to access metrics<a name="tag-metrics"></a>

You need one of the following **Analytics and Optimization** security profile permissions: 
+ **Access metrics \- Access**
+ **Real\-time metrics \- Access**, as shown in the following image of the **Analytics and Optimization** section of the security profiles page\.

![\[The Real-time metrics - Access permission on the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-tag-based-access-control-perm.png)

When you enable **Access metrics \- Access**, permissions are also automatically granted to **Real\-time metrics **, ** Historical metrics**, and **Agent activity audit**\. The following image shows all of these permissions granted\.

**Note**  
When users have all of these permissions, they can see all data for historical metrics for which  tag\-based access controls are not currently applied\.

![\[The Access metrics - Access permission on the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-tag-based-access-control-perm-2.png)

### Permissions to access resources<a name="tag-metrics"></a>

The following image shows an example of security profile permissions that grant users the ability to view routing profiles, queues, and Amazon Connect user accounts\. **Routing profiles \- View**, **Queues \- View**, and **Users \- View** are selected\.

![\[The routing section and users and permissions section of the security profiles page.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/rtm-tag-based-access-control-perm-3.png)

## Functionality limitations<a name="rtm-tag-based-access-control-limitations"></a>

The following limitations apply to tag\-based access controls for real\-time metrics\.

1. You can only filter and group tables by the primary resource \(user, queue, or routing profile\)\. You cannot filter and group tables by non\-primary resources\. For example, you cannot filter by queue in an agent table and you cannot group by queue in a routing profile table\.

1. Drill\-down button disabled within tables except for **View queue graphs**\. For example, you cannot choose **View agents** in a queue table\.

1. Access to the homepage service level dashboard is disabled\.

1. Access to view **Agent Queues** is disabled\.

1. **Agent Adherence** table is not yet  supported\.

## Transitioning to tag\-based access control<a name="rtm-tag-based-access-control-transitioning"></a>

If you open a saved report containing tables with users, queues, or routing profiles that you don't have access to anymore due to tag\-based access control, or if groupings or non\-primary filters are applied to tables, you won't see data in those tables\. 

To view the data, do one of the following steps:
+ Edit your table filters to include the agents, queues, or routing profiles that you have access to\.
+ Create a new report that includes the resources you have access to\.
+ Remove the groupings and non\-primary filters from the table\.