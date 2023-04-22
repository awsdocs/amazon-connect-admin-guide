# Generate, review, and publish a schedule by using Schedule Manager<a name="scheduling-publish-schedule"></a>

Amazon Connect is designed to generate the least number of shifts for agents based on the forecasted demand pattern and configured constraints to hit the optimization goal\.

After you create shift activities, shift profiles, staffing groups and staffing group rules, you can generate a schedule\. 

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Scheduling**, **Schedule manager \- Edit**\. 

   For more information, see [Security profile permissions for forecasting, capacity planning, and scheduling](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Scheduling**\.

1. Choose the **Schedule Manager** tab, and then choose **Generate schedule**\. 

1. Enter a name and description for the schedule\.

1. In the **Schedule input** section, select the forecast group from the dropdown menu\.

   Currently you cannot schedule for multiple forecast groups\.

1. Specify the duration of the schedule \- the start and end dates\. You can schedule up to 18 weeks out\.

1. Under **Optimize schedule for**, choose **Service level** or **Average speed of answer**\.

1. Average speed of answer \(ASA\) is an alternative to using service level percentage targets\. For example, the following image shows an ASA set to 30 seconds\. The capacity planning and scheduling system will optimize headcount / schedules to ensure that the goal is met\.  
![\[The Generate schedule page, the schedule input section, the average speed of answer option set to 30 seconds.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/asa-gen-schedule.png)

1. Choose **Generate schedule**\.
**Note**  
Amazon Connect generates a draft schedule\. It will not be visible to agents or supervisors until you publish it\.

1. In the list of schedules, the schedule you created shows a status of **In progress**\. It takes 5\-30 minutes to generate, depending on the number of agents, number of configured rules, schedule duration, and more\. After the schedule is generated, it's status is **Complete** or **Failed**\.

1. To view any warnings, breaches of rules, or constraints breaches, choose the warnings icon, as shown in the following image\. More information about the warnings is displayed\.  
![\[The schedule calendar, the warnings icon, an example of schedule warnings.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-scheduling-warnings.png)

1. When the status is **Complete**, choose the draft schedule to view it\. The following image shows a sample schedule for one day, for 10 agents\.  
![\[A sample schedule for 10 agents.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-scheduling-supervisors-schedule.png)

   Schedulers can:
   + View schedules for all agents\.
   + Pick a date to view a specific shift\.
   + Navigate back to today's date\.
   + View failed rules and goals\.

1. When you're satisfied with the schedule, choose **Publish**\. You'll get a confirmation page\. Choose **Proceed** to make the schedule official\!   
![\[A schedule page, the Publish button, the Proceed button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-scheduling-publish-confirmation.png)

   Staff \(agents\) and supervisors specified in the staffing groups can now view the schedule\. See the following topics to learn about their experience: 
   + [How supervisors view published schedules](scheduling-view-schedule-supervisors.md)
   + [How agents view their schedule](scheduling-view-schedule-agents.md)

## Edit a schedule<a name="scheduling-edit-schedule"></a>

Before publishing a schedule, you might want to edit it\. For example, if you notice that all the agents are scheduled to be on break at the same time and no one is scheduled to take contacts\.

You can: 
+ Change agent shift start and/or end time, duration\.
+ Change activity shift start and/or end time, duration\.
+ Add an activity to one or more agents shift\.
+ Remove or replace activity from an agent shift\.
+ Copy an entire shift from one agent to another\.
+ Recompute metrics to ensure schedule adjustments result in better service level \(SL%\) or occupancy\.

The following image shows these options in the dropdown list: **Edit**, **Add**, **Replace**, **Remove**, **Copy**\.

![\[A dropdown list of actions you can perform on a schedule before it is published.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-scheduling-edit-schedule.png)

## Regenerate a schedule<a name="scheduling-regenerate-schedule"></a>

Managers and supervisors can regenerate agent schedules for up to six different forecast groups after making changes to the scheduling configuration\.

1. To edit a schedule, select the schedule, choose **Actions**, and select **Edit Schedules**\. Make your changes and choose **Save**\.

1. To regenerate one or more schedules, select the schedules you want to regenerate, choose **Actions**, and select **Regenerate schedules**\.

## Search and sort a schedule<a name="scheduling-manager-search-sort"></a>

Managers and supervisors can search and sort schedules from within the schedule manager\. Schedulers can search for schedule names using partial keywords or sort the schedule list based on start date, end date, creation date, or updated date\.

The following image shows the search box on the **Scheduling** page\. Entering **mar** returns schedules that have March in their name\.

![\[The scheduling page, the search box.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/scheduling-manager-search-sort-example.png)