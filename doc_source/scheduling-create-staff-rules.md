# Create staff rules for scheduling<a name="scheduling-create-staff-rules"></a>

Use staff rules to specify optional details for individual agents and supervisors, such as their local time zone, start and end dates, and contract details\. 
+ The individual staff rules you specify here override any staffing group rules when their schedule is generated\. 

For example, you might set up the staffing group to generate a schedule where everyone works 40 hours per week\. In the staff rules, you can choose specific employees to schedule for 20 hours per week\.

**To create staff rules for individual users**

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Scheduling**, **Schedule manager \- Edit**\. 

   For more information, see [Assign permissions](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Scheduling**\.

1. On the **Scheduling** page, choose the **Staff Rules** tab, and then search and choose one or more staff from the list\. Every time a staff is selected, the staff count is displayed in the **Apply to Staff** button\.

1. Specify optional details such as:
   + **Time zone**: Render schedules in the local time zone of the agent\.
   + **Shift start and end dates**: Schedule specific agent shifts based on start or end dates\.
   + **Working hours and minutes**: Define the minimum and maximum working hours per day and per week\. Working hours should include non\-productive time, such as breaks and meals\. 

     For example: 
     + If you want to generate agent schedules that are 8 hours and 30 minutes long each day, then specify 8 hours and 30 minutes in both **min** and **max** working hour fields\.
     + If you want to allow the system to generate more efficient schedules, you may provide a **min** and **max** working hours window\. The system will generate the most optimal schedule duration based on forecasts and agent availability\.
   + **Consecutive days worked or days off**: Schedule shifts based on the allowed range of consecutive days worked or days off\. 
   + **Associate to shift profile**: You can assign a shift profile to individual agents\. This is useful to do when, for example, you have part\-time agents who are in the same staffing group as your full\-time agents, but they require their own shift profile\. 

     The following image shows the location of the **Associate to shift profile** dropdown menu on the **Staff rules** tab\.  
![\[The staff rules tab, the associate to shift profile dropdown menu.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-scheduling-staffrules-tab3.png)

1. Choose **Apply to Staff**\. This saves the rules, and ensures they are applied during the next scheduling cycle\. 