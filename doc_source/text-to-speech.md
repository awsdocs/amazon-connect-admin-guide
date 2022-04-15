# Add text\-to\-speech to prompts<a name="text-to-speech"></a>

You can enter text\-to\-speech prompts in the following contact flow blocks: 
+ [Get customer input](get-customer-input.md) 
+ [Loop prompts](loop-prompts.md)
+ [Play prompt](play.md)
+ [Store customer input](store-customer-input.md)

## Amazon Polly converts text\-to\-speech<a name="amazon-polly-default-voice-free"></a>

To convert text\-to\-speech, Amazon Connect uses Amazon Polly, a service that converts text into lifelike speech using SSML\. 

Amazon Polly default voices are **free**\. You are charged only for using custom voices that are associated with your account\.

## Amazon Polly best sounding voice<a name="amazon-polly-best-sounding-voice"></a>

Amazon Polly periodically releases improved voices and speaking styles\. You can choose to automatically resolve your text\-to\-speech to the most lifelike and natural sounding variant of a voice\. For example, if your contact flows use Joanna, Amazon Connect automatically resolves to Joanna’s conversational speaking style\. 

**Note**  
If no Neural version is available, Amazon Connect defaults to the standard voice\. 

**To automatically use the best sounding voice**

1. Open the Amazon Connect console at [https://console\.aws\.amazon\.com/connect/](https://console.aws.amazon.com/connect/)\.

1. If prompted to login, enter your AWS account credentials\.

1. Choose the name of the instance from the **Instance alias** column\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/instance.png)

1. In the navigation pane, choose **Contact flows**\.

1. In the Amazon Polly section, choose **Use the best available voice**\.

## How to add text\-to\-speech<a name="add-tts"></a>

1. In a contact flow, add the block that will play the prompt\. For example, add a [Play prompt](play.md) block\. 

1. In the **Properties**, choose **Text\-to\-speech**\. 

1. Enter plain text, as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-sample-tts.png)

   Or enter SSML:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-sample-ssml.png)

SSML\-enhanced input text gives you more control over how Amazon Connect generates speech from the text you provide\. You can customize and control aspects of speech such as pronunciation, volume, and speed\.

For a list of SSML tags you can use with Amazon Connect, see [SSML tags supported by Amazon Connect](supported-ssml-tags.md)\. 

For more information about Amazon Polly, see [Using SSML](https://docs.aws.amazon.com/polly/latest/dg/ssml.html) in the Amazon Polly Developer Guide\.