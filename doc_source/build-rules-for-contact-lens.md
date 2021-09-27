# Build rules with Contact Lens<a name="build-rules-for-contact-lens"></a>

Contact Lens rules allow you to automatically categorize contacts, receive alerts, or generate tasks based on uttered keywords, sentiment scores, customer attributes, and other criteria\. 

## Step 1: Define rule conditions<a name="rule-conditions"></a>

1. On the navigation menu, choose **Rules**\.

1. Select **Create a rule**, **Contact Lens**\.

1. Assign a name to the rule\.

1. Under **When**, use the dropdown list to choose **post\-call analysis** or **real\-time analysis**\.

1. Choose **Add condition**\. 

   You can combine criteria from a large set of conditions to build very specific Contact Lens rules\. Following are the available conditions: 
   + **Words or phrases**: Choose from [Exact match, Pattern match, or Semantic match](exact-match-pattern-match-semantic-match.md) to trigger an alert or task when keywords are uttered\.
   + **Agent**: Build rules that run on a subset of agents\. For example, create a rule to ensure newly hired agents comply with company standards\.

     To see agent names so you can add them to rules, you need **Users \- View** permissions in your security profile\. 
   + **Queues**: Build rules that run on a subset of queues\. Often organizations use queues to indicate a line of business, topic, or domain\. For example, you could build rules specifically for your sales queues, tracking the impact of a recent marketing campaign or alternatively rules for your customer support queues, tracking overall sentiment\.

     To see the queue names so you can add them to rules, you need **Queues \- View** permissions in your security profile\. 
   + **Contact attributes**: Build rules that run on the values of custom [contact attributes](what-is-a-contact-attribute.md)\. For example, you can build rules specifically for a particular line of business or for specific customers, such as based on their membership level, their current country of residence, or if they have an outstanding order\. 

     You can add up to five contact attributes to a rule\.
   + **Sentiment \- Time period**: Build rules that run on the sentiment analysis results \(positive, negative, or neutral\) over a trailing window of time\. For example, you can build a rule for when customer sentiment has remained negative for a set period of time\.
   + **Sentiment \- Entire contact**: Build rules that run on the value of sentiment scores over an entire contact\. For example, you can build a rule when customer sentiment has remained low for the entire contact, you can create a task for a customer experience analyst to review the call transcript and follow\-up\.
   + **Interruptions**: Build rules that detect when the agent has interrupted the customer for more than X times\. 
   + **Non\-talk time**: Build rules that run when periods of no talk time are detected\. For example, when a customer and agent have not spoken for over 30 seconds which may indicate unnecessary customer wait time or highlight a customer services process that would benefit from optimisation\. 

   Following is a sample rule with multiple conditions\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rules-conditions.png)

1. Choose **Next**\.

### Step 2: Define rule actions<a name="rule-actions"></a>

1. Under **Assign contact category**, enter a category name\.
**Note**  
In this step, you are naming a required rule action: **Assign Contact Category**\. The action is to categorize all contacts based on the category name you create\. The category name is reflected in the Contact Lens output\. 

1. Choose **Add action**\. Since you already named **Assign Contact Category**, it's not available\. You can choose the following:
   + [Generate an EventBridge event](contact-lens-rules-eventbridge-event.md)
   + [Create task](contact-lens-rules-create-task.md)  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-action.png)

1. Choose **Next**\.

1. Review and make any edits, then choose **Save**\. 

1. After you add rules, they are applied to new contacts that occur after the rule was added\. Rules are applied when Contact Lens analyzes conversations\.

   You cannot apply rules to past, stored conversations\. 