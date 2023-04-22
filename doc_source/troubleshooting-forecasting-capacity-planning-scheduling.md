# Troubleshooting forecasting, capacity planning, and scheduling<a name="troubleshooting-forecasting-capacity-planning-scheduling"></a>

These sections outline troubleshooting scenarios and address frequently asked questions for forecasting, capacity planning, and scheduling\.
+ [Forecasting](#troubleshooting-forecasting)
+ [Capacity planning](#troubleshooting-cap-planning)
+ [Scheduling](#troubleshooting-scheduling)

## Forecasting<a name="troubleshooting-forecasting"></a>
+ **How can I create an ad hoc forecast?**

  Forecasts are processed automatically, delivering short\-term forecasts daily, and long\-term forecasts weekly, so users don’t need to worry about running forecasts manually\. However, you may want to see how a forecast is updated when you add or modify historical data\. For example, if you had an anomaly in your historical contact volume, and you don’t want the machine\-learning model to use that anomaly in building a forecast, you can modify the historical data and then when the new forecasts are run, the new forecasts will not incorporate that data\.

  To see the most recent forecasts, check the **Last computed** column\.

  New forecasts will be generated when a user uploads or deletes historical data using the **Import data** tab or adds/removes queues from a forecast group\.  
![\[Data on the Forecasts tab, the Last computed column.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/faq-adhoc-forecast.png)
+ **When I import historical data it returns errors\.**

  Select **download details** to ensure that the imported data is in the correct format: If there are any errors, check the error details\. It will provide additional details for the specific error\. You must ensure that your file is in `.csv` format, contains no decimals, no extra rows, or column fields\. For more information on the required format, see [Import historical data for forecasting](https://docs.aws.amazon.com/connect/latest/adminguide/import-data-for-forecasting.html)\.  
![\[Failed status message, download details link.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/faq-import-historical-data.png)
+ **Forecast failed due to error: Insufficient data in Amazon Connect\.**

  When you receive this error, it could be due to three different reasons:

  1. *You have less than 6 month of historical data\.* To address this problem, upload more historical data\. While Amazon Connect can generate forecasts with six months of data, we recommend at least 12 months of recent contact data to ensure that contact patterns \(for example, seasonality\) are properly captured\. If you don’t have 6 months of data, you can give Connect synthetic \(artificial\) data that will be used to generate the forecast\. Alternately, you can upload your own forecast using the **Override** function\.

  1. *You need at least 2,000 contacts per month across all of your forecast groups\.* Amazon Connect generates forecasts using historical data for all queues that are included across all forecast groups\. At least 2,000 monthly contacts in the past 6 months for the Amazon Connect instance are required to successfully generate a forecast\. Amazon Connect does not require 2,000 monthly contacts for every queue\. All queues in all forecast groups must total more than 2,000 monthly contacts\.

  1. *You need recent data\.* Amazon Connect performs a data recency check \(is the data recent enough\) based on the aggregation of all queues included across all forecast groups\. At least one data point in the past four weeks is required to successfully generate a forecast\.
+ **Cannot import data, cannot download forecast, cannot create forecast group, or cannot create forecast\.**

  Most likely, you do not have the correct permissions\. Check with your admin to ensure you have permissions for **Analytics, Forecasting \- Edit**\.
+ **Forecasting override upload failed\.**

  Check the error message to make sure the `.csv` file format matches our data schema\. For more information on the required format, see [Import historical data for forecasting](https://docs.aws.amazon.com/connect/latest/adminguide/import-data-for-forecasting.html)\.
**Tip**  
download the computed or published forecast `.csv` file\. Take the time period for override, and copy the queue ID and queue name, time stamps to the override template\. Note, only the latest uploaded `.csv` file will be used, and the previous uploaded files will be overridden\.
+ **Long\-term Forecast failed even after I have uploaded more than 6 months of data\.**

  The data uploads for long\-term and short\-term forecasts are independent, so you will need to upload these separately: one for long\-term and one for short\-term\. First, check if you also uploaded the daily historical data for long\-term forecast\. The 15 to 30 minute interval data is for short\-term forecasts only\. Second, check if the long\-term daily level `.csv` file has more than 6 consecutive months historical data counted from now\.
+ **Short\-term forecast failed even after I uploaded more than 6 month of data\.**

  The data uploads for long\-term and short\-term forecasts are independent\. The daily interval data is for long\-term forecast only\. First, check if you uploaded the 15 or 30 minute interval historical data for short\-term forecast and the file has more than 6 consecutive month data\. Second, check what is the forecast interval setting in `.csv` file to ensure it matches the historical intervals on the UI\.
+ **Why am I unable to publish a forecast?**

  It’s possible that you do not have permissions to publish a forecast\. It’s also possible that the forecasts \(both contact volume and handle time for each of short\-term and long\-term\) have not been successfully generated\. Check if you have the permission for **Analytics, Forecasting \- Publish** and check if the forecasts have been successfully generated \(the status column should show **complete”** when the forecasts are generated\)\.
+ **How can I see data from a previous period?**

  You are able to view forecasts in a specified period that occurred in the past\.  
![\[Short term tab, calendar to choose the duration.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/faq-past-forecast.png)
+ **Can I see past forecast data?**

  You can see the last published and the last computed forecast\. The last computed forecast will be overwritten once the next forecast is computed\. If you wish to retain this data, you can download the `.csv` file that contains the last computed and published forecasts\.
+ **Why are the forecasts used in capacity planning different than the ones I see in forecasting or scheduling?**

  The forecast that is used in capacity planning is the most recent published long\-term forecast\. You may see a different forecast in forecasting if you are looking at the most recent computed forecast in comparison to a published forecast\. You will see a different forecast in scheduling, as that is the most recently published short\-term forecast\.
+ **Why do I see the call volume peak in short\-term forecast at mid\-night when no traffic is expected?**

  Forecasting uses Coordinated Universal Time \(UTC\) as its time zone\. For North American users on the Pacific or Atlantic Coasts, this is 8 hours ahead of PST, or 7 hours ahead of PDT; and 5 hours ahead of EST, or 4 hours ahead of EDT\. So for example, midnight in UTC is 4pm PST / 5pm PDT or 7pm EST / 8pm EDT\.
**Note**  
It’s important to remember to use UTC time when uploading historical data or overrides\.
+ **Why am I unable to delete a forecast?**

  Forecasts can only be deleted if they are not being used for a capacity plan \(long\-term forecast\) or schedule \(short\-term forecast\)\. Check if the forecast has been published and that it is used for scheduling or capacity planning\. You must delete the schedule or capacity plans in order to delete the forecast\.
+ **Why do the long\-term and short\-term forecasts show different values for the same time period?**

  These two forecasts have different training frequencies and different models, as they are optimized for different purposes\. Short\-term is designed for interval level granularity over a period of weeks and long\-term is designed for daily granularity over a period of months\.
+ **Why is long\-term average handle time flat but short\-term average handle time isn't?**

  A flat average handle time performs better when forecasting short\-term forecast workloads as it displays interval granularity over a period of weeks\. Allowing the average handle time to vary in a long\-term forecast results in better performance as displays daily granularity over a period of months\.

  Handle time is important when calculating a workload\. It generally doesn’t vary much in the short term but can vary over longer time periods, which is reflected in our models\.
+ **Is call volume counted at the time when the call comes in, or when the call ends?** 

  Call volume starts counting at the time when call comes in\. For example\. a call started at 4:50 PM, and ends at 5:05 PM\. It will be counted as the call volume for the 4:45 PM \- 5:00 PM interval\.

## Capacity planning<a name="troubleshooting-cap-planning"></a>
+ **How do I handle shrinkage in capacity planning?**

  Users can increase capacity planning accuracy by providing estimated future data, which includes available full\-time employees \(FTE\) and Shrinkage, for the existing forecast groups\. Providing Available FTE and shrinkage data is optional\. Amazon Connect can generate a capacity plan without it but providing it improves the accuracy of the capacity plan\. In order to import that data, download the `.csv` template from the UI and fill out the empty cells\. Note that users need to enter the exact name of the forecast groups they created\. Also, users can add multiple forecast groups in this `.csv` file\. For more information, see [Import estimated future shrinkage and available full\-time employees](https://docs.aws.amazon.com/connect/latest/adminguide/upload-estimated-future-shrinkage.html)\.
+ **I am seeing errors during data import in capacity planning\.**

  Confirm that the forecast group names in the `.csv` file match the actual forecast group names in forecasting module\.

## Scheduling<a name="troubleshooting-scheduling"></a>
+ **The system does not generate schedules for some or all of my agents\. What should I check?**

  This can occur due to the fact that the last date an agent can be scheduled is before the time of the schedule and/or the agent's maximum working hours don’t allow them to work in that shift profile\. Review the following steps to address this issue\.

  1. Check **Staff Rules** to ensure that the **End date** is not configured for agents who do not have a schedule\. **End date** allows schedulers to specify the last date that an agent can be scheduled until\.

  1. Check shift profiles to see if the **Start time** and **End time** hourly schedule window is equal to or more than **Maximum working hours** per agent\. For example, if the shift profile is configured to generate a schedule of an 8 hour duration, when the agent’s staff rule is configured for them to work 4 hours per day, the system will apply the staff rule and only generate a schedule for 4 hours\.
+ **Why am I unable to access the scheduling page while on my company's VPN?**

  It is possible that your company's VPN has security measure in place that could be preventing access to the needed endpoints\. If you are unable to access the scheduling page while connected to your company's VPN, reach out to your admin or network security team to have them allowlist the following endpoints:

  ```
  .awsapps.com/connect/markov/schedule-ui/api/graphql
  ```

  ```
  .my.connect.aws/markov/schedule-ui/api/graphql
  ```
+ **Why are lunch activities for some agents scheduled before the first break activity, even though I have specified a lunch activity to be placed after the break?**

  This can be caused by having overlaps in the break and lunch activities\. Check the specific shift profile to see if the placement window for both activities overlap\. For example, you may have configured a break activity to be placed between 11am and 1pm and a lunch activity to be placed between 10am and 3pm, so the system may choose to place the break at 12:30pm and the lunch at 11:30am\. Remove or minimize the overlap of activity placement windows to solve this issue\.
+ **Why do I see agents get scheduled at different start times than expected?**

  This is commonly caused by challenges with time zones\. Shift profiles are set using Coordinated Universal Time \(UTC\), and staff rules specify which time zone agents should use\. Review the following steps to address this issue\.
  + Ensure the **shift profile** start time and end time are configured in the UTC time\-zone\.
  + Ensure the correct user time\-zones are set in the **Staff rules** UI\. For example, if you want to schedule agents in Boston \(EST time\-zone\) from 9am to 5pm, you must do the following\.
    + Set **Shift profile** start time as 1:00pm and end time as 9pm\. Usually shift profiles are set once and later re\-used\.
    + Updated the timezone for all agents to EST time zone in the **Staff rules** UI\.
+ **Can I view the schedule in my local time?**

  Yes\. Supervisors and schedulers can view schedules in their local time zone for agents they manage\. Agents can view their individual schedules in their local time zone\. User time zones can be set in the **Staff rules** UI\.
+ **Do I need to define activities for workloads like phone or chat?**

  No\. *Work* will be the default activity on the schedule if there is no break or lunch scheduled for the time slot\. Only define the activities for the agent when they are not taking a call or responding to a chat\.
+ **Why did some agents did not get added to the roster for certain days?**

  How agents are added to the roster depends on multiple configurations in staffing groups and staff rules, such as min/max working hours, min staff required, or min/max consecutive work days\. The service will take the defined working hours and add an agent to the roster by taking into consideration other rules that have been defined in staffing groups and staff rules\. For example, if the minimum working hours are 40 hours, and the agent belongs to a staff group that operates 12 hours per day and 6 days per week, then the agent is likely to have some days without schedules\. The service optimizes schedules based on forecasts\. As long as the minimum amount of 40 hours per week \(4 days with 10 hours per day\) is met, the agent may not be staffed on some days when the call volume is low\. In cases where you see that an agent doesn't have a schedule for a day, check the agent's minimum working hours\. Also, check if the agent has been added to the roster for the remainder of the week\.
+ **Why is my agent's scheduled time different than the shift profile time? For example, my shift profile has 10 hours every weekday, but my agent only gets scheduled for 6 hours?**

  The shift profile operation hours apply to staffing groups\. If you don’t set the staffing groups rule for **shift start time**, the service will optimize your agent start time based on the forecasted workload\. For example, the shift profile has 8 AM \- 6 PM Monday \- Friday, and the workload is light in the morning, and heavier in the afternoon\. Each agent has a minimum of 6 hours and a maximum of 8 hours per day\. To save agent cost, the service will schedule less agents in the morning and more agents in the afternoon\. Some agents could start at 8 AM, some could start at 8:30 AM, and some could start in the afternoon\. Some agents could have 6 hour schedules and some could have 8 hour schedules\. In this way, you can maximize your agent resources to meet the service goal\. If you want every agent to start at the same time and work an exact number of hours, you can set the rule in the staffing group **shift start time** to **start at the same time** and set the **working hour** to 10 hours every day\. In this case, savings on agent cost will be less due to less flexibility to optimize based on forecasts\.  
![\[Rules for working time, minimum staff required, and shift start time.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/faq-different-schedule-rules.png)
+ **My agents are all full\-time employees and they work 8 hours per day\. How can I set this up in my schedule?**

  Set your staffing group's and staff's maximum and minimum working hours to 8 hours a day\.
+ **I have a mix of full\-time and temporary employees\. What is the best way to define it?**

  The best practice is to use staffing groups to set the working hours to the 8 hours and then use staff rules to set the individual part\-time agent working hours to their specific value\. The value in the staff rule will override the value in the staffing group\.
+ **How do I add meetings or one\-off events?**

  Generate a schedule with daily activities first\. In the schedule manager view, select any schedule, and use **add shift** to add a one\-off shift activity to the schedule\.