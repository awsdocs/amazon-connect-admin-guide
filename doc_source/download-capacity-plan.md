# Download a capacity plan<a name="download-capacity-plan"></a>

When you download a capacity plan file, it downloads as a \.csv file type with multiple tabs\. It's helpful to open this file using Excel\. The following image shows an example of what a capacity plan file looks like in Excel\. It has the following worksheets: Metrics, Capacity Plan, Scenario, Generation Details\.

![\[A downloaded capacity plan file opened with Excel.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wfm-capacity-planning-download1.png)

Following is a description of each worksheet:
+ **Metrics**: The capacity plan output\.
+ **Capacity Plan**: The capacity plan metadata, such as name, starting date, and ending date of the plan\.
+ **Scenario**: The input defined for the capacity plan\. 
+ **Generation Details**: The metadata indicating when someone last changed the capacity plan\.

## How to download capacity plan results<a name="howto-download-capacity-plan"></a>

1. Log in to the Amazon Connect console with an account that has security profile permissions for **Analytics**, **Capacity planning \- Edit**\. 

   For more information, see [Security profile permissions for forecasting, capacity planning, and scheduling](required-optimization-permissions.md)\. 

1. On the Amazon Connect navigation menu, select **Analytics and optimization**, **Capacity Planning**\.

1. On the **Capacity Plans** tab, choose the plan\. 

1. On the detailed page for the capacity plan, choose **Actions**, **Download capacity plan**\. 