# Review capacity plan output \(Preview\)<a name="capacity-planning-review-output"></a>

To review capacity plan output, choose the hyperlink for the plan you generated\. The first half of the page summarizes the input you used in scenario and capacity plan generation\. 

The plan output shows a week\-by\-week or month\-by\-month calculation\. To switch from weekly to monthly view, select **Monthly** from the dropdown, as shown in the following image\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-capacity-planning-output3.png)

Following is a description of the metrics in the plan output:
+ **Forecasting Inputs**
  + **Forecasted Contact Volume**: This metric is a sum of both voice and chat volume for the selected forecast group\. 
  + **Forecasted Average Handling Time \(AHT\), seconds**: This metric shows the aggregated AHT for the selected forecast group\.
+ **Outputs**
  + **Required FTEs \(without Shrinkage\)**: How many full\-time equivalent agents need to be hired to meet the defined business goals \(such as service level target\), without considering shrinkage\. 
  + **Forecasted Occupancy %**: How much occupancy is for the agents\.
+ **Outputs with additional input**
  + **Required FTEs \(with Shrinkage\)**: How many full\-time equivalent agents needed to be hired to meet the defined business goals \(such as service level target\), with considering shrinkage\.
  + **Available FTEs**: How many agents are available for working that day\. It can be uploaded in the **Import data** section\.
+ **Metrics calculated from available FTE input**
  + **Gap between available FTEs and required FTEs**: The difference between available FTEs and required FTEs\. 
  + **Gap %**: The percentage of the gap\.
  + **Required OT %**: if there is a supply deficit \(required FTEs higher than available FTEs\), required OT% indicates how much overtime would be needed to cover the deficit\. 
  + **Required OT %**: If there is a supply surplus \(the number of required FTEs is lower than the available FTEs\), required VTO % indicates how much voluntary time off could be used to lower the amount of agent idle time and thus lower costs\.