# Set the Hours of Operation for a Queue<a name="set-hours-operation"></a>

The first thing you need to do when you set up a queue is to specify the hours of operation\. The hours may be referenced in contact flows\. For example, when routing contacts to agents, you might use the [Check Hours of Operation](check-hours-of-operation.md) block first, and then route the contact to the appropriate queue\. 

**To set the hours of operation for a queue**

1. Choose **Routing**, **Hours of operation**\.

1. To create a template, choose **Add new hours** and enter a name and a description\.

1. For **Time zone**, select a value\.

1. For **Add new**, set new hours\.

1. Choose **Save**\.

1. Now you can specify these the hours of operation when you [create a queue](create-queue.md), and check them in the [Check Hours of Operation](check-hours-of-operation.md) block\.

## How to Specify Midnight<a name="set-hours-operation-midnight"></a>

To specify midnight, enter 12:00AM\.

For example, if you want to set your hours to 10:00AM to midnight, you would enter: 10:00AM to 12:00AM\. Your call center would be open for 14 hours\. Here's the math: 
+ 10:00AM\-12:00PM = 2 hours
+ 12:00PM\-12:00AM = 12 hours
+ Total = 14 hours

## Examples<a name="set-hours-operation-examples"></a>

**Schedule for 24x7**

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-hours-of-operation-24x7.png)

**Schedule for Monday to Friday 9:00 AM to 5:00 PM**

Remove Sunday and Saturday from the schedule\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-hours-of-operation-closed-weekends-remove.png)

The final schedule looks like this: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-hours-of-operation-closed-weekends.png)

## Use the Check Hours of Operation Block<a name="use-check-hours-of-operation-block"></a>

At the start of your contact flows, use the [Check Hours of Operation](check-hours-of-operation.md) block to determine whether your contact center is open, and to branch accordingly\. 