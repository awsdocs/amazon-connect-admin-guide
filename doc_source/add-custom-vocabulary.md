# Add custom vocabularies<a name="add-custom-vocabulary"></a>

You can improve the accuracy of speech recognition for product names, brand names, and domain\-specific terminology, by expanding and tailoring the vocabulary of the speech\-to\-text engine in Contact Lens\. 

This topic explains how to add custom vocabularies using the Amazon Connect console\. You can also add them using the [CreateVocabulary](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateVocabulary.html) and [AssociateDefaultVocabulary](https://docs.aws.amazon.com/connect/latest/APIReference/API_AssociateDefaultVocabulary.html) APIs\. 

## Things to know about custom vocabularies<a name="things-to-know-about-cust-vocab"></a>
+ You must set a vocabulary as the **default** for it to be applied to the analyses to generate transcripts\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-custom-vocab-default.png)
+ You can have one vocabulary per language applied to the analyses\. This means only one file per language can be in the **Ready \(default\)** state\.
+ You can upload more than 20 vocabulary files\. However, you can activate only 20 custom vocabulary files at the same time\.
+ Transcription is a one\-time event\. A newly uploaded vocabulary isn't applied retroactively to existing transcriptions\.
+ Your text file must be in LF format\. If you use any other format, such CRLF format, your custom vocabulary is not accepted by Amazon Transcribe\.
+ For limits to the size of a vocabulary file and other requirements, see [Custom vocabularies](https://docs.aws.amazon.com/transcribe/latest/dg/custom-vocabulary.html) in the *Amazon Transcribe Developer Guide*\.
+ Custom vocabularies apply to speech analytics only\. They do not apply to chat conversations because the transcripts already exist\. 

## Required permissions<a name="add-custom-vocabulary-permissions"></a>

Before you can add custom vocabularies to Amazon Connect, you need the **Analytics and Optimization**, **Contact Lens \- custom vocabularies** permission assigned to your security profile\.

By default, in new instances of Amazon Connect the **Admin** and **CallCenterManager** security profiles have this permission\.

For information about how add more permissions to an existing security profile, see [Update security profiles](update-security-profiles.md)\.

## Add a custom vocabulary<a name="how-to-add-custom-vocabulary"></a>

1. Log in to Amazon Connect with a user account that has the required permissions to add custom vocabularies\.

1. Navigate to **Analytics and optimization**, **Custom vocabularies**\.

1. Choose **Add custom vocabulary**\.

1. On the **Add custom vocabulary** page, enter a name for the vocabulary, choose a language, and then choose **Download a sample** file\.

   The following image shows what the sample file looks like:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-custom-vocab-header.png)

1. The information in the file is separated by one \[TAB\] per entry\. For details about how to add words and acronyms to your vocabulary file, see [Creating a custom vocabulary using a table](https://docs.aws.amazon.com/transcribe/latest/dg/custom-vocabulary-create-table.html) in the *Amazon Transcribe Developer Guide*\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-custom-vocab-phrase-column.png)

   To enter multiple words in the **Phrase** column, separate each word with a hyphen \(\-\); do not use spaces\. 

## Vocabulary states<a name="about-cust-vocab-states"></a>
+ **Ready \(default\)**: The vocabulary is being applied to the analyses to generate transcripts\. It is applied to both real\-time and post\-call analyses\.
+ **Ready**: The vocabulary is not being applied to analyses, but it is a valid file and available\. To apply it to analyses, set it to default\. 
+ **Processing**: Amazon Connect is validating your uploaded vocabulary and trying to apply it to the analyses to generate transcripts\.
+ **Deleting**: You chose to **Remove** the vocabulary, and Amazon Connect is deleting it now\. 

  It takes about 90 minutes for Amazon Connect to delete a vocabulary\.

If you attempt to upload a vocabulary that does not validate, it results in a **Failed** state\. For example, if you add multiple\-word phrases to the **Phrase** column, and separate them with spaces instead of hyphens, it will fail\. 

## Download and view a custom vocabulary<a name="view-custom-vocabulary"></a>

To view a custom vocabulary that has been uploaded, you download and open the file\. Only files in the **Ready** state can be downloaded and viewed\.

1. Navigate to **Analytics and optimization**, **Custom vocabularies**\.

1. Choose **More**, **Download**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-custom-vocab-download.png)

1. Open the download to view the contents\.

1. You can change the contents, and then choose **Save and upload**\. 