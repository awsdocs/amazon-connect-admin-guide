# Set your "Next status" in the CCP<a name="set-next-status"></a>

**Note**  
"Next status" is available only to customers who are using the latest Contact Control Panel \(CCP\)\. The URL for the latest CCP ends with **ccp\-v2**\.  
**IT administrators**: For more information about the **Next status** feature, such as changes to the agent event stream, see [July 2021 Updates](amazon-connect-release-notes.md#july21-release-notes) in the *Release notes*\. 

Use the **Next status** feature to pause new contacts being routed to you, while you finish your current contacts\. When all your slots are cleared, Amazon Connect automatically sets your CCP to the next status, such as **Lunch**\.

The following images of the Contact Control Panel \(CCP\) show how to use this feature\.

![\[\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/next-status-example-new.png)

1. Available: The agent is on a contact\.

1. The agent chooses their next status, such as **Lunch**\. They can choose only a custom \([NPT](real-time-metrics-definitions.md#non-productive-time-real-time)\) status, or **Offline**\. 

1. The agent is in **Next status: Lunch**\. They are still on contact\. No new contacts can be routed to them\. 

1. The contact ends\. The agent finishes ACW, and chooses **Clear contact**\. Instead of going back to **Available**, their CCP is automatically set to **Lunch**\. 

## How to cancel "Next status"<a name="next-status-example"></a>

You can easily switch from **Next status** back to **Available**\. The ability to switch your status is useful, for example, if you accidentally choose **Next status: Lunch**, or if you decide not to go to **Lunch** before Amazon Connect automatically sets to that status\. 

The following images show this workflow\.

![\[The CCP set to next status, the CCP set to available.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/next-status-example-cancel.png)

1. While working on the same contact, the agent cancels **Next status: Lunch** and goes back to **Available**\.

1. The contact ends and the agent is still **Available** for new contacts to be routed to them\. 

## Example 1: Set "Next status" while handling only ACW contacts<a name="next-status-examples-acw"></a>

Let's say an agent is finishing after contact work \(ACW\) for one or more contacts, such as a voice contact or multiple chats\. They are not on contact with anyone\.

Instead of choosing **Clear contact** when the agent finishes ACW, they choose **Lunch**\. This puts them in **Next status: Lunch** only briefly\. 

Here's what happens in this scenario:

1. Agent finishes ACW and chooses **Lunch** instead of **Clear contact**\.

1. Amazon Connect stops routing new contacts to them\.

1. All their slots are cleared\. This is so the agent doesn't have to choose **Clear contact** to end the ACW\. 

1. Because all the ACWs have been cleared, Amazon Connect immediately starts the automatic transition that sets the agent's status to **Lunch**\.

   Agents were put into **Next status \- Lunch** only briefly \(milliseconds\!\)\. They might even see it in the CCP if they look fast enough\. 

This order of events mirrors how the CCP works when agents change their status while working on ACW\. For example, an agent is finishing ACW and they set their status to **Lunch**\. Here's what happens next:

1. Amazon Connect stops routing new contacts to them\.

1. The ACW slot is cleared for the agent so they don't have to choose **Clear contact**\. 

1. The agent is set to **Lunch**\.

## Example 2: Set "Next status" while managing some chats on contact and other chats in ACW<a name="next-status-examples-oncontact"></a>

Let's say an agent is managing two chats: 
+ Customer 1 is in ACW\.
+ Customer 2 is on contact\.

While still on a contact, the agent sets their status to **Offline**\. This puts them in the **Next status: Offline** state\. 

Here's what happens in this scenario:

1. The agent sets their status to **Offline**\.

1. Amazon Connect stops routing new contacts to them\.

1. The contact that is in ACW is cleared so the agent doesn't have to choose **Clear contact**\. Only the connected chat remains\.

1. The agent's status is **Next status: Offline**, and they continue working on their connected chat\.

1. After they finish work on that contact, the agent chooses **Clear contact** to end the ACW\. 

1. Amazon Connect automatically sets the agent's status to **Offline**\.