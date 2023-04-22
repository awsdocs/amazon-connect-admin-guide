# Automatically categorize contacts based on uttered keywords and phrases<a name="rules"></a>

You can set up Contact Lens to track issues that you know exist in your contact center \("known knowns"\), and monitor any changes over time\. 

You can label your contacts based on predefined criteria you set up, that is, keywords and phrases you want to detect\. Through categorization, each contact is analyzed for these criteria, and labeled\. 

This is useful to do when, for example, you want to ensure that agents are using certain words or phrases in calls or chats, for compliance reasons\. Or, for example, you want to investigate when customers use certain words and have a negative sentiment\. 

To set up this feature, add rules that contain the words or phrases that you want to highlight\.

In a **Contact details** page for a chat, categories appear above the transcript, as shown in the following image\. 

![\[The contact details page, the categories section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-overview-chat2.png)

The following image shows what a **Contact details** page looks like with a category for a call\. The category is named **cancellation**\. It contains the words or phrases you want to highlight in the analysis\.

![\[The contact details page, a category for a call.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-overview2.png)

## Add rules to categorize contacts<a name="add-category-rules"></a>

### Step 1: Define conditions<a name="add-category-rules-define-conditions"></a>

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for **Rules** permissions\.

1. On the navigation menu, choose **Analytics and optimization**, **Rules**\. 

1. Select **Create a rule**, **Contact Lens**\. 

1. Assign a name to the rule\.

1. Under **When**, use the dropdown list to choose **post\-call analysis**, **real\-time analysis**, or **post\-chat analysis**\.  
![\[The new rule page, the when dropdown list.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-rule-define-conditions.png)

1. Choose **Add condition**, and then choose the type of match: 
   + **Exact Match**: Finds only the exact words or phrases\. Enter the words or phrases, separated by a comma\.
   + **Semantic Match**: Finds words that may be synonyms\. For example, if you enter "upset" it can match "not happy," or "hardly acceptable" can match with "unacceptable," and "unsubscribe" can match with "cancel subscription\." 

     Similarly, it can semantically match phrases\. For example, "thank you so much for helping me out," "thanks a lot and this is so helpful," and "I am so happy that you are able to help me\."

     This removes the need to define an exhaustive list of keywords while creating categories, and provides you the ability to cast a wider net for searching similar phrases that are important to you\.

     For best semantic matching results, provide keywords or phrases with similar meaning within a semantic matching card\. Currently, you can provide a maximum of four keywords and phrases per semantic matching card\.
   + **Pattern Match**: Finds matches that may be less than 100 percent exact\. You can also specify the distance between words\. For example, if you are looking for contacts where the word "credit" was mentioned but you do not want to see any mention of the words "credit card," you can define a pattern matching category to look for the word "credit" that is not within a one\-word distance of "card\." 

1. Using **Exact Match** as an example, enter the words or phrases, separated by a comma, that you want to highlight\.  
![\[The new rules page, the Words or phrases - Exact match section.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script.png)

1. Choose **Add**\. Each word or phrase separated by a comma gets its own line in the card\.  
![\[The new rules page, the Words or phrases - Exact match section, the Add button.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script2.png)

   The logic that Contact Lens uses to read these phrases is: \(Hello OR thank OR you OR for OR calling OR Example OR Corp\) OR \(we OR value OR your OR business\) OR \(how OR may OR I OR assist OR you\)\.

1. To add more words or phrases, choose **Add group of words or phrases**\. In the following image, the first group of words or phrases are what the agent might utter, and the second group is what the customer might utter\.  
![\[A Words or phrases - Exact match for agent, the word AND, a Words or phrases section for the customer.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script3.png)

   1. In this first card, Content Lens reads each line as an OR\. For example: \(Hello OR thank OR you OR for OR calling OR Example OR Corp\) OR \(we OR value OR your OR business\) OR \(how OR may OR I OR assist OR you\)\.

   1. The two cards are connected with an AND\. This means, one of the rows in the first card needs to be uttered AND then one of the phrases in the second card needs to be uttered\.

   The logic that Contact Lens uses to read the two cards of words or phrases is \(card 1\) AND \(card 2\)\.

1. Choose **Add condition** to apply the rules to:
   + Specific queues
   + When contact attributes have certain values
   + When sentiment scores have certain values

   For example, the following image shows a rule that applies when an agent is working the BasicQueue or Billing and Payments queues, the customer is for auto insurance, and the agent is located in Seattle\.  
![\[A rule with multiple conditions.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-3.png)

### Step 2: Define actions<a name="add-category-rules-define-actions"></a>

In addition to categorizing a contact, you can define what actions Amazon Connect should take: 

1. [Generate an EventBridge event](contact-lens-rules-eventbridge-event.md)

1. [Create Task](contact-lens-rules-create-task.md)

1. [Send email notifications](contact-lens-rules-email.md)

### Step 3: Review and save<a name="add-category-rules-review-save"></a>

1. When done, choose **Save**\. 

1. After you add rules, they are applied to new contacts that occur after the rule was added\. Rules are applied when Contact Lens analyzes conversations\.

   You cannot apply rules to past, stored conversations\. 