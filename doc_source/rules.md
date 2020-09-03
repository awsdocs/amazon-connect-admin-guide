# Automatically categorize contacts based on uttered keywords and phrases<a name="rules"></a>

You can set up Contact Lens to analyze conversations for certain words or phrases, and then highlight where they are uttered in the conversation\. This is useful to do when, for example, you want to ensure that agents are speaking certain words or phrases for compliance reasons\. Or, for example, you want to investigate when customers use certain words and have a negative sentiment\. 

To set up this feature, you add rules that contain the word or phrases you want to highlight\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-category-overview.png)

## Security profile permissions for Contact Lens rules<a name="permissions-for-rules"></a>

To view, edit, or add rules for automatic categorization, you must be assigned to a security profile that has **Rules** permissions\. For more information, see [Security profile permissions for Contact Lens](permissions-for-contact-lens.md)\.

## How to add rules<a name="add-category-rules"></a>

1. Log in to Amazon Connect with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for **Rules** permissions\.

1. In Amazon Connect choose **Metrics and quality**, **Rules**\.

1. Assign a name to the rule\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules.png)

1. Enter the words or phrases, separated by a comma, that you want to highlight\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script.png)

1. Choose **Add**\. Each word or phrase separated by a comma gets its own line\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script2.png)

   The logic that Contact Lens uses to read these words or phrases is: \(Hello\) OR \(thank OR you OR for OR calling OR Example OR Corp\) OR \(we OR value OR your OR business\), etc\.

1. To add more words or phrases, choose **Add group of words or phrases**\. In the following image, the first group of words or phrases are what the agent might utter, and the second group is what the customer might utter\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-add-category-rules-script3.png)

   The logic that Contact Lens uses to read the two groups of words or phrases is \(group 1\) AND \(group 2\)\.

1. When done, choose **Save**\. 

1. After you add the rules, they are applied in real time to **new** contacts when Contact Lens analyzes conversations\. You can't analyze past, stored conversations\.

## Tips for adding rules<a name="tips-for-adding-rules"></a>

Following are some tips for adding rules:
+ It's an exact word match, singular or plural\.
+ AND OR are allowed\.
+ To enter a script, enter phrases\. For example, if you want to highlight when agents say *Thank you for being a member\. We appreciate your business*, enter two phrases: 
  + Thank you for being a member\.
  + We appreciate your business\.

## Rules are applied to new contacts<a name="rules-applied-to-new-contacts"></a>

After you add the rules, they are applied in real time to **new** contacts when Contact Lens analyzes conversations\. You can't analyze past stored conversations\.