# Delete your Amazon Connect instance<a name="delete-connect-instance"></a>

If you no longer need your contact center, you can delete your Amazon Connect instance\. When you delete an instance, we release its claimed phone number back to inventory\. When customers call the phone number that you've released, they'll get a message that it's not a working phone number\.

**Important**  
You can't restore a deleted instance or access its settings, data, metrics, and reports\.

## Delete your instance<a name="delete-cconnect-instance-procedure"></a>

**To delete your Amazon Connect instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Select the radio button for the instance\.

1. Choose **Delete**\. If you don't see the **Delete** button, you don't have permissions to delete instances\. Contact your AWS administrator for help\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance-delete.png)

1. When prompted, enter the name of the instance and then choose **Delete**\.

**Tip**  
We recommend checking your CloudWatch log groups related to the Amazon Connect instance, and deleting them if they are no longer needed\. For more information, see [Delete a CloudWatch Logs log group using an AWS SDK](https://docs.aws.amazon.com/AmazonCloudWatch/latest/logs/example_cloudwatch-logs_DeleteLogGroup_section.html)\. 

## Error message: "Region Unsupported\. Amazon Connect is not available in \[Region\]"<a name="region-unsupported"></a>

If you get this error message, it means that you selected a Region in the AWS Management Console that is not the Region in which you created the Amazon Connect instance, and Amazon Connect isn't available in that Region\.

**To switch Regions and delete your Amazon Connect instance**

1. From the navigation bar, open the Region selector\. Select the Region in which you created the Amazon Connect instance\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/aws-management-console-region.png)

1. From the navigation bar, choose **Amazon Connect** from the list of services to open the Amazon Connect console\. If you don't see the instance, keep selecting from the supported Regions until you find your instance\.

1. Select the radio button for the instance\.

1. Choose **Delete**\. If you don't see the **Delete** button, you don't have permissions to delete instances\. Contact your AWS administrator for help\.

1. When prompted, enter the name of the instance and then choose **Delete**\.