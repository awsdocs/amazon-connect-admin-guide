# Create staff scheduling rules<a name="scheduling-create-staff-rules"></a>

Use staff rules to specify details for individual agents and supervisors, such as their local time zone, start and end dates, and contract details\. The individual staff rules you specify here override any staffing group rules when their schedule is generated\.

For example, you might set up the staffing group to generate a schedule where everyone works 40 hours per week\. In the staffing rules, you can choose specific employees to schedule for 20 hours per week\.

**To create staffing rules for individual users**

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Scheduling**, **Schedule manager \- Edit**\. 

   For more information, see [Required permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Users**, **Scheduling**\.

1. Choose the **Staff Rules** tab, and then search and choose one or more staff from the list\. 

1. Specify details such as:
   + Time zone: Render schedules in the local time zone of the agent\.
   + Start and end dates: Schedule specific agent shifts based on start or end dates\.
   + Working hours: Define the minimum and maximum working hours per day and per week\. Working hours should include non\-productive time, such as breaks and meals\.
   + Consecutive days worked or days off: Schedule shifts based on the allowed range of consecutive days worked or days off\. 

1. Choose **Apply to Staff**\. This saves the rules, and ensures they are applied during the next scheduling cycle\. 