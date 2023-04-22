# Create rules with Contact Lens<a name="build-rules-for-contact-lens"></a>

Contact Lens rules allow you to automatically categorize contacts, receive alerts, or generate tasks based on uttered keywords, sentiment scores, customer attributes, and other criteria\. 

This topic explains how to create rules using the Amazon Connect console\. To create and manage rules programmatically, see [Rules actions](https://docs.aws.amazon.com/connect/latest/APIReference/rules-api.html) and the [Amazon Connect Rules Function language](https://docs.aws.amazon.com/connect/latest/APIReference/connect-rules-language.html) in the *Amazon Connect API Reference Guide*\. 

**Tip**  
For a list of rules feature specifications \(for example, how many rules you can create\), see [Amazon Connect Rules feature specifications](feature-limits.md#rules-feature-specs)\.

## Step 1: Define rule conditions<a name="rule-conditions"></a>

1. On the navigation menu, choose **Analytics and optimization**, **Rules**\.

1. Select **Create a rule**, **Contact Lens**\.

1. Under **When**, use the dropdown list to choose **post\-call analysis**, **real\-time analysis**, or **post\-chat analysis**\.  
![\[The new rule page, the when dropdown menu.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rule-define-conditions.png)

1. Choose **Add condition**\. 

   You can combine criteria from a large set of conditions to build very specific Contact Lens rules\. Following are the available conditions: 
   + **Words or phrases**: Choose from [Exact match, Pattern match, or Semantic match](exact-match-pattern-match-semantic-match.md) to trigger an alert or task when keywords are uttered\.
   + **Agent**: Build rules that run on a subset of agents\. For example, create a rule to ensure newly hired agents comply with company standards\.

     To see agent names so you can add them to rules, you need **Users \- View** permissions in your security profile\. 
   + **Queues**: Build rules that run on a subset of queues\. Often organizations use queues to indicate a line of business, topic, or domain\. For example, you could build rules specifically for your sales queues, tracking the impact of a recent marketing campaign or alternatively rules for your customer support queues, tracking overall sentiment\.

     To see the queue names so you can add them to rules, you need **Queues \- View** permissions in your security profile\. 
   + **Contact attributes**: Build rules that run on the values of custom [contact attributes](what-is-a-contact-attribute.md)\. For example, you can build rules specifically for a particular line of business or for specific customers, such as based on their membership level, their current country of residence, or if they have an outstanding order\. 

     You can add up to five contact attributes to a rule\.
   + **Sentiment \- Time period**: Build rules that run on the sentiment analysis results \(positive, negative, or neutral\) over a trailing window of time\. 

     For example, you can build a rule for when customer sentiment has remained negative for a set period of time\. If the participant joined the contact later, the time period set here applies to when participant was present\.
   + **Sentiment \- Entire contact**: Build rules that run on the value of sentiment scores over an entire contact\. For example, you can build a rule when customer sentiment has remained low for the entire contact, you can create a task for a customer experience analyst to review the call transcript and follow\-up\.
   + **Interruptions**: Build rules that detect when the agent has interrupted the customer for more than X times\. This feature applies to calls only\. 
   + **Non\-talk time**: Build rules that run when periods of no talk time are detected\. For example, when a customer and agent have not spoken for over 30 seconds which may indicate unnecessary customer wait time or highlight a customer services process that would benefit from optimisation\. This feature applies to calls only\.
   + **Response time**: Build rules to identify contacts where the participant had a response time longer or shorter than what was expected: Average or Maximum\. 

     For example, you can set a rule on the **Agent greeting time**, also known as **First response time**: after the agent joined the chat, how long until they sent the first greeting message\. This will help you to identify when an agent took too long to engage with the customer\.

   The following image shows a sample rule with multiple conditions for a voice contact\.  
![\[A sample rule with multiple conditions for a voice contact.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-conditions.png)

   The following image shows a sample rule with multiple conditions for a chat contact\. The rule is triggered when the **First** response time is greater than or equal to 1 minute, and the agent did not mention any of the listed greeting words or phrases in their first response\.

   **First response time** = after the agent has joined the chat, how long until they sent the first message to the customer\.   
![\[A sample rule with multiple conditions for a chat contact.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-conditions-chat.png)

1. Choose **Next**\.

## Step 2: Define rule actions<a name="rule-actions"></a>

1. Under **Assign contact category**, enter a category name\.
**Note**  
In this step, you are naming a required rule action: **Assign Contact Category**\. The action is to categorize all contacts based on the category name you create\. The category name is reflected in the Contact Lens output\. And, you can use it for [contact search](search-conversations.md#contact-category-search)\. 

1. Choose **Add action**\. Since you already named **Assign Contact Category**, it's not available\. You can choose the following actions:
   + [Generate an EventBridge event](contact-lens-rules-eventbridge-event.md)
   + [Create Task](contact-lens-rules-create-task.md)
   + [Send email notifications](contact-lens-rules-email.md)  
![\[The add action dropdown menu, a list of actions.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-action-no-wisdom.png)

1. Choose **Next**\.

1. Review and make any edits, then choose **Save**\. 

1. After you add rules, they are applied to new contacts that occur after the rule was added\. Rules are applied when Contact Lens analyzes conversations\.

   You cannot apply rules to past, stored conversations\. 