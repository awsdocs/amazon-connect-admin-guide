# Create staffing groups and rules<a name="scheduling-create-staffing-groups"></a>

A *staffing group* is a group or team of agents who are skilled to take specific types of contacts\. You add agents who need a schedule generated for them, and supervisors who manage agent schedules\. You can also add rules that apply at the staffing group level, such as the minimum staff required and the minimum working hours per day or week for the group\. If a user meeds to view published agent schedules from the **Published** calendar view, then the user must be added as a supervisor within the specific staffing group\.

For example, say your contact center opens at 9AM but the forecast says no contacts arrive between 9\-9:30AM\. You can add a rule that says, despite what the forecast predicts, there should be a minimum of one agent during this time\. 

If you don't have a shift start time rule, then the schedule is built using the predictions from the forecast\.

For a list of staffing group limits, see [Forecasting, capacity planning, and scheduling feature specifications](feature-limits.md#forecasting-cap-planning-scheduling-specs)\.

## Example<a name="example-staffing-groups"></a>

For example, you might create one staffing group named General Enquiry, and another named Tier 2 Support\.  Because you map one or more staffing groups to a forecast group, here's how you would create staffing groups in this case:

1. Group all General Enquiry queues to a General Enquiry forecast group\.

1. Map the General Enquiry forecast group to multiple staffing groups that have agents who can take general enquiry contacts\.

## Create group and add staff<a name="staffing-groups-add-staff"></a>

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Scheduling**, **Schedule manager \- Edit**\. 

   For more information, see [Security profile permissions for Forecasting, capacity planning, and scheduling](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Scheduling**\.

1. Choose the **Staffing Groups** tab, and then choose **Create staffing group**\.

1. On the **Create Staffing Group** page, under **Associate to forecast group**, use the dropdown to choose the forecast group to associate with this staffing group\. 

   In the following example, contacts from the queues in the Forecast\_Group\_20220124 will be routed to the agents in this staffing group\.

1. Choose **Add staff** to add agents and supervisors to this staffing group\. A user must be added to Amazon Connect in order to appear in the list of staff\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-scheduling-add-staff.png)
**Tip**  
Every agent must be in a staffing group in order for a schedule to be generated for them\. You can add and remove agents in between schedule cycles and manually add shifts\. 

## Add rules<a name="staffing-groups-add-rules"></a>

To generate a schedule, Amazon Connect uses information from the forecast group, which reflects the historical demand pattern for your contact center\. Staffing rules enable you to specify conditions that must be accounted for in the schedule, regardless of what the forecast predicts\.

For example, your contact center opens at 9AM but the forecast says no contacts arrive between 9AM\-9:30AM\. You can add a rule that, despite what the forecast predicts based on historical demand, there should be a minimum of one agent during this time\. This forces Amazon Connect to keep one agent in the schedule from 9\-9:30AM\. In addition, you can add a rule to set the **Working Hours** to start at 9AM, even though the forecast would start it at 9:30AM\.

**To add rules**
+ In the **Rules** section, choose **\+** and then use the dropdown to choose the type of rule to create for the staffing group\. For example, you can specify:
  + **Minimum Staff Required**: Specify the minimum number of agents that should be available, despite what the forecast indicates\. For example, if the forecast says that you do not need any agents in the first half hour that your contact center opens, you can ensure that there is a minimum of one agent during this time\. 
  + **Shift Start Time: Same Start Time**: This creates schedules with the same shift start time for all agents\.
  + **Working Hours**: Specify the group's minimum and maximum working hours per day or week\. This setting applies to all staff in the staffing group\. You can override this setting for individual staff\. For instructions, see [Create staff scheduling rules](scheduling-create-staff-rules.md)\. 