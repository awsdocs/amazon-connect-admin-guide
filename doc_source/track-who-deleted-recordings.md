# Track who deleted or listened to recordings<a name="track-who-deleted-recordings"></a>

You need an AWS account to do these steps\.

## Set up logging<a name="setup-logging-of-deleted-recordings"></a>

1. If you have multiple instances and buckets, look up the name of the Amazon S3 bucket for your instance\. Go to the Amazon Connect console, choose the instance alias, and choose **Data storage**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/s3-bucket-name.png)

1. Go to the Amazon S3 console\.

1. Choose the Amazon S3 bucket where your recordings are stored\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/s3-recordings-bucket.png)

1. Choose the **Properties** tab\.

1. Choose **Object\-level logging** and then choose **View CloudTrail trails**\. 

   It opens the AWS CloudTrail console\. 

1. In the navigation menu, choose **Trails** and then choose the trail name\. 

1. In the upper right corner, toggle **Logging** to **ON**, if it's not on already\. 

1. Under **Management** events, choose the edit icon\. To log only who deletes recordings, you set this to **Write\-only**\. To also log who listens to recordings, set to **All**\. Choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/s3-bucket-management-events.png)

1. Under **CloudWatch Logs** choose the edit icon\. Either accept the default name for your log group \(CloudTrail/DefaultLogGroup\), or specify a new name\. Choose **Continue**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-cw-logs.png)

1. Choose **Allow**\. You can now close the AWS CloudTrail console\.

## Find who deleted or listened to recordings<a name="find-who-deleted-recordings"></a>

1. Go to the Amazon CloudWatch console\.

1. Choose **Create dashboard**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cw-create-dashboard.png)

1. Enter a name, such as **CloudTrail\-logging**\.

1. On the **Add to this dashboard** dialog box, choose **Query results**\. Choose **Configure**\.

1. In the **Select log groups**, use the drop\-down arrow to choose the log group for your instance, such as **CloudTrail/DefaultLogGroup**\.

1. In the query box, delete the current query, and then copy and paste the one shown below instead\. This query will find all API events where the recording was deleted: 

   ```
                       fields @timestamp, @message
                       | filter eventSource ='s3.amazonaws.com'
                       | filter eventName = 'DeleteObject'
   ```

1. In the time box, choose how far back you want to search\.

1. Choose **Run query**\.

   It returns all of the events that are named **DeleteObject**\.

1. Next to the event, choose the arrow\. It expands to show you detailed information about the event, including the ID of the user who deleted the recording\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/cw-deletion-event.png)

1. If a lot of records are returned, choose the **Actions** arrow, and then choose **Download query results \(CSV\)**\. The data is exported to Excel\. From there you can format the spreadsheet so it's easier for you to search and see the names of the users who deleted recordings\.

   The following image shows what the @message column looks like in the CSV file\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/deleted-call-recording-record.png)

1. If you're also logging who listened to recordings, update the query to search for the eventName **GetBucketLocation**\.

   ```
                       fields @timestamp, @message
                       | filter eventSource ='s3.amazonaws.com'
                       | filter eventName = 'GetBucketLocation'
   ```

## Tips<a name="track-who-deleted-recordings-tips"></a>

Mirroring CloudTrail logs to CloudWatch is useful but optional\. Mirroring the CloudWatch log allows you to use CloudWatch Insight to search the events easily\.

If you have a large contact center, you may not want to use object logging because it generates many logs that are stored in your Amazon S3 bucket\.

Another option is to write an AWS Lambda function to process the CloudTrail events\. You can also search the logs manually\. 