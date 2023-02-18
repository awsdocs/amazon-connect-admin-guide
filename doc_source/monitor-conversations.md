# Set up live monitoring for voice and/or chat<a name="monitor-conversations"></a>

Managers and agents in training can monitor live conversations between agents and customers\. To set this up, you need to add the **Set recording behavior** block to your voice/chat flow, assign managers and trainees the appropriate permissions, and then show them how to monitor the conversations\.

**Looking for how many people can monitor the same conversation at one time?** See [Amazon Connect feature specifications](feature-limits.md)\.

There is no limit to the number of conversations that can be monitored in an instance\. 

## Add a Set recording and analytics behavior block to your flow<a name="monitor-conversations-set-up"></a>

1. Add the [Set recording and analytics behavior](set-recording-behavior.md) block to your flow\. Do this to monitor calls, chats, or both\. 

   To enable monitoring of voice and/or chat conversations, in the block's properties choose **Agent and Customer**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-recording-and-analytics-behavior1.png)

   For more information, see [Set up recording behavior](set-up-recordings.md)\. 

1. Choose whether to record the conversations you monitor\. 

   Although you need to add the **Set recording behavior** block to your flow, you don't need to record voice and/or chat conversations for monitoring to work\. By default when you set up your instance, [Amazon S3 buckets are created](amazon-connect-instances.md#get-started-data-storage) to store call recordings and chat transcripts\. The existence of these buckets enables call recording and chat transcripts at the instance level\. 

   To not record the calls or chats you're monitoring, disable the Amazon S3 buckets\. For instructions, see [Update instance settings](update-instance-settings.md)\.