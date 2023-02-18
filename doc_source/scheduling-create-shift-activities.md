# Create shift activities<a name="scheduling-create-shift-activities"></a>

Shift activities are daily activities that the staff \(agents\) does during their shift\. For example:
+ **Productive**: At work activities that agents do that are counted as productive work, such as answering contacts\.
+ **Non\-Productive**: At work activities that agents do that are not counted as productive work, such as breaks and team meetings\.
+ **Time off**: Absent from work\. Their status in the agent application is **Offline**\.

You can create multiple shift activities to include as part of your staff shifts\.

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Scheduling**, **Schedule manager \- Edit**\. 

   For more information, see [Security profile permissions for Forecasting, capacity planning, and scheduling](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Scheduling**\.

1. Choose the **Shift Activities** tab, and then choose **Add shift activities**\. Fill in the details and choose **Save**\. 

   You can add multiple activities, and add and remove activities\.

1. The next time a schedule is created as part of the scheduling cycle, the shift activities are applied\.

**Tip**  
Create shift profiles to ensure the desired sequence of the shift activities\. For example, to schedule agents to go on their break two hours before lunch\. For instructions, see [Create shift profiles](scheduling-create-shift-profiles.md)\.