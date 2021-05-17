# Delete your instance<a name="delete-connect-instance"></a>

If you no longer want to use an instance, you can delete it\. When you delete an instance, the phone number claimed for the instance is released back to inventory\. You lose all settings, data, metrics, and reports associated with the instance\. When customers call the phone number you've released, they'll get a message that it's not a working phone number\.

**Important**  
You cannot undo the deletion of an instance or restore settings or data from the instance after it is deleted\.

**To delete an instance**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. Select the check box for the instance and choose **Remove**\. If you don't see the **Remove** button, you don't have permissions to delete instances\. Contact your AWS administrator for help\.

1. When prompted, type the name of the instance and choose **Remove**\.

## Error message: "Region Unsupported\. Amazon Connect is not available in \[Region\]"<a name="region-unsupported"></a>

If you get this error message, it means you created the Amazon Connect instance in a Region different than the one you're in now, such as US East \(Ohio\), and Amazon Connect isn't available in that Region\. 

**To switch Regions to the Amazon Connect instance**

1. At the AWS Management console, switch your Region to US East \(Virginia\) or whichever Region you were in when you created the Amazon Connect instance\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/aws-management-console-region.png)

1. Choose **Amazon Connect** to open the Amazon Connect console\.

1. You'll see the Amazon Connect instance and can delete it\. If you don’t see the instance, go back to the AWS Management Console and choose another Region, such as US West \(Oregon\), and then do steps 2 and 3\. 