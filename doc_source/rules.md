# Automatically categorize contacts based on uttered keywords and phrases<a name="rules"></a>

You can set up Contact Lens to track issues that you know exist in your contact center \("known knowns"\), and monitor any changes over time\. 

You can label your contacts with predefined criteria you set up, that is, keywords and phrases you want to detect\. Through categorization, each contact is analyzed for these criteria, and labeled\. 

This is useful to do when, for example, you want to ensure that agents are speaking certain words or phrases for compliance reasons\. Or, for example, you want to investigate when customers use certain words and have a negative sentiment\. 

To set up this feature, add rules that contain the words or phrases that you want to highlight\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-overview.png)

## Security profile permissions for Contact Lens rules<a name="permissions-for-rules"></a>

To view, edit, or add rules for automatic categorization, you must be assigned to a security profile that has **Rules** permissions\. For more information, see [Security profile permissions for Contact Lens](permissions-for-contact-lens.md)\.

## Add rules to categorize contacts<a name="add-category-rules"></a>

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for **Rules** permissions\.

1. On the navigation menu, choose **Rules**\. 

1. Select **Create a rule**, **Contact Lens**\. 

1. Assign a name to the rule\.

1. Next to **When**, use the dropdown list to choose **post\-call analysis** or **real\-time analysis**\.

1. Choose **Add condition**, and then choose the type of match: 
   + **Exact Match**: Finds only the exact words or phrases\.
   + **Semantic Match**: Finds words that may be synonyms\. For example, if you enter "upset" it can match "not happy," or "hardly acceptable" can match with "unacceptable," and "unsubscribe" can match with "cancel subscription\." 

     Similarly, it can semantically match phrases\. For example, "thank you so much for helping me out," "thanks a lot and this is so helpful," and "I am so happy that you are able to help me\."

     This removes the need to define an exhaustive list of keywords while creating categories, and provides you the ability to cast a wider net for searching similar phrases that are important to you\.

     For best semantic matching results, provide keywords or phrases with similar meaning within a semantic matching card\. Currently, you can provide a maximum of four keywords and phrases per semantic matching card\.
   + **Pattern Match**: Finds matches that may be less than 100 percent exact\. You can also specify the distance between words\. For example, if you are looking for contacts where the word "credit" was mentioned but you do not want to see any mention of the words "credit card," you can define a pattern matching category to look for the word "credit" that is not within a one\-word distance of "card\." 

1. Enter the words or phrases, separated by a comma, that you want to highlight\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script.png)

1. Choose **Add**\. Each word or phrase separated by a comma gets its own line in the card\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script2.png)

   The logic that Contact Lens uses to read these words or phrases is: \(Hello\) OR \(thank OR you OR for OR calling OR Example OR Corp\) OR \(we OR value OR your OR business\), etc\.

1. To add more words or phrases, choose **Add group of words or phrases**\. In the following image, the first group of words or phrases are what the agent might utter, and the second group is what the customer might utter\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script3.png)

   1. In this first card, Content Lens reads each line as an OR\. For example: \(Hello\) OR \(thank OR you OR for OR calling OR Example OR Corp\) OR \(we OR value OR your OR business\)\.

   1. The two cards are connected with an AND\. This means, one of the rows in the first card needs to be uttered AND then one of the phrases in the second card needs to be uttered\.\.

   The logic that Contact Lens uses to read the two cards of words or phrases is \(card 1\) AND \(card 2\)\.

1. When done, choose **Save**\. 

1. After you add the rules, they are applied in real time to **new** contacts when Contact Lens analyzes conversations\. You can't analyze past, stored conversations\.

## Tips for adding rules<a name="tips-for-adding-rules"></a>

Following are some tips for adding rules\.

### How to enter a script<a name="enter-script"></a>

To enter a script, enter phrases\. For example, if you want to highlight when agents say *Thank you for being a member\. We appreciate your business*, enter two phrases: 
+ Thank you for being a member\.
+ We appreciate your business\.

### How to use exact match<a name="exact-match"></a>

**Exact Match** really is an exact word match, singular or plural\.

### How to use pattern match<a name="pattern-match"></a>

If you want to match related words, append an asterisk \(\*\) to the criteria\. For example, if you want to match on all variations of "neighbor" \(neighbors, neighborhood\) you would type **neighbo\***\.

With **Pattern Match** you can specify the following:
+ **List of values**: This is useful when you want to build expressions with interchangeable values\. For example, the expression might be: 

  *I'm calling about a power outage in \["Beijing" or "London" or "New York" or "Paris" or "Tokyo"\]*

  Then in your list of values you would add the cities: Beijing, London, New York, Paris, Tokyo\. 

  The advantage of using values is that you can create one expression, instead of multiple\. This reduces the number of cards that you need to create\.
+ **Number**: This option is used most frequently in compliance scripts, or if your looking for a context when you know somewhere in between there's a number\. This way you can put all of your criteria into one expression instead of two\. For example, an agent compliance script might say:

  *I have been in this industry for \[num\] years and would like to discuss this topic with you\.*

  Or a customer might say: 

  *I have been a member for \[num\] years\.*
+ **Proximity definition**: Finds matches that may be less than 100 percent exact\. You can also specify the distance between words\. For example, if you are looking for contacts where the word "credit" was mentioned but you do not want to see any mention of the words "credit card," you can define a pattern matching category to look for the word "credit" that is not within a one\-word distance of "card\."

  For example, a proximity definition might be:

  *credit\* \[is not within 0 to 1 word apart\] card\**

### How to use semantic match<a name="semantic-match"></a>

Semantic matching is supported only for post\-call analysis\.
+ An “intent” is an example of utterance\. It can be a phrase or a sentence\.
+ You can enter up to four intents in one card \(group\)\.
+ We recommend using semantically similar intents within one card to get the best results\. For example, there's category for "politeness\." It includes two intents: "greetings" and "goodbye"\. We recommend separating these intents into two cards:
  + Card 1: "How are you today" and "How’s everything going"\. They are semantically similar greetings\.
  + Card 2: "Thanks for contacting us" and "Thank you for being our customer\." They are semantically similar goodbyes\.

  Separating the intents into two cards provides more accuracy than putting them all into one card\.

## Rules are applied to new contacts<a name="rules-applied-to-new-contacts"></a>

After you add the rules, they are applied in real time to **new** contacts when Contact Lens analyzes conversations\. You can't analyze past, stored conversations\.