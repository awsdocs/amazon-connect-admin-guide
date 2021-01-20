# Alert supervisors real\-time based on keywords and phrases<a name="add-rules-for-alerts"></a>

After you [enable real\-time analytics](enable-analytics.md) in your contact flow, you can add rules that automatically alert supervisors when a customer experience issue occurs\. 

For example, Contact Lens can automatically send an alert when certain keywords or phrases are uttered during the conversation, or when it detects other criteria\. The supervisor sees the alert on the real\-time metrics dashboard\. From there, supervisors can listen in to the live call, and provide guidance to the agent over chat to help them resolve the issue faster\.

The following image shows an example of what a supervisor would see on the real\-time metrics report when they get an alert\. In this case, Contact Lens has detected an angry customer situation\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-real-time-metrics-alert.png)

When the supervisor listens in to a live call, Contact Lens provides them with a real\-time transcript and customer sentiment trend that helps them understand the situation and assess the appropriate action\. The transcript also eliminates the need for customers to repeat themselves if the call is transferred to another agent\. Following is a sample real\-time transcript\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-real-time-transcript.png)

## Security profile permissions for Contact Lens rules<a name="permissions-for-rules-alerts"></a>

To view, edit, or add rules, you must be assigned to a security profile that has **Rules** permissions\. For more information, see [Security profile permissions for Contact Lens](permissions-for-contact-lens.md)\.

## Add rules for real\-time alerts<a name="add-category-rules-real-time"></a>

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for **Rules** permissions\.

1. On the navigation menu, choose **Rules**\. 

1. Select **Create a rule**, **Contact Lens**\. 

1. Assign a name to the rule\.

1. Next to **When**, use the dropdown list to choose **real\-time analysis**\.

1. Choose **Add condition**, and then choose the type of match: 
   + **Exact Match**: Finds only the exact words or phrases\.
   + **Pattern Match**: Finds matches that may be less than 100 percent exact\. You can also specify the distance between words\. For example, you might look for contacts where the word "credit" was mentioned, but you do not want to see any mention of the words "credit card\." You can define a pattern matching category to look for the word "credit" that is not within a one\-word distance of the word "card\." 
**Tip**  
Semantic Match isn't available for real\-time analysis\.

1. Enter the words or phrases, separated by a comma, that you want to highlight\. Real\-time rules only support any keywords or phrases that **were mentioned**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-alert-rules-1.png)

1. Choose **Add**\. Each word or phrase separated by a comma gets its own line\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-alert-rules-2.png)

   The logic that Contact Lens uses to read these words or phrases is: \(Talk OR to OR your OR manager\) OR \(this OR is OR not OR helpful\) OR \(speak OR to OR your OR supervisor\), etc\.

1. To add more words or phrases, choose **Add group of words or phrases**\. In the following image, the first group of words or phrases are what the agent might utter\. The second group is what the customer might utter\.  
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

With **Pattern March** you can specify the following:
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

## Rules are applied to new contacts<a name="rules-applied-to-new-contacts-alerts"></a>

After you add the rules, they are applied in real time to **new** contacts when Contact Lens analyzes conversations\. You can't analyze past stored conversations\.