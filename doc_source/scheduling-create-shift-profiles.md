# Create shift profiles<a name="scheduling-create-shift-profiles"></a>

Use shift profiles to create templates for weekly shifts\. The template includes the days of the week worked, the earliest start time and the latest end times the staff can be scheduled, and the activities they would do during their shift\. 

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Scheduling**, **Schedule manager \- Edit**\. 

   For more information, see [Security profile permissions for forecasting, capacity planning, and scheduling](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Users**, **Scheduling**\.

1. Choose the **Shift Profiles** tab, and then choose **Add shift profiles**\. 

1. Select days of the week staff will be scheduled for, earliest start time and the latest end time for each day\. Ensure that these times are configured in UTC instead of local time\.

   Depending on the contact demand pattern forecast, Amazon Connect determines the best possible start and end times for shifts, while adhering to the minimum and maximum hours per day and week worked\.

1. Choose **Add shift activities**\. Select the shift activities the staff will do during their shift\.

1. For each activity, set placement rules\. The rules include:
   + The time duration from the beginning to end of the shift where the activities need to be placed\.
   + The time window for Amazon Connect to pick the best spot to maximize efficiency of the generated schedules to meet the goals, such as the service level percent \(SL%\) targets\.

1. After saving the shift profile, you can edit or remove it from the list view\.

For example, if you set break to start 6 hours after the start of a shift and lunch to start 3 hours after the start of a shift, the lunch is scheduled to occur first\.

