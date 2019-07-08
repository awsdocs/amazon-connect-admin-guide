# Create Prompts<a name="prompts"></a>

Prompts are audio files played in call flows\. For example, hold music is a prompt\. Amazon Connect comes with a set of prompts that you can add to your contact flows\. Or, you can add your own recordings\. 

Only 8 KHz \.wav files that are less than 50 MB are supported for prompts\. You can upload a pre\-recorded \.wav file to use for your prompt, or record one in the web application\. 

We recommend that you align your prompts and routing policies with each other to ensure a smooth call flow for customers\.

**To create a prompt**

1. In the navigation pane, choose **Routing**, **Prompts**\.

1. On the **Manage voice prompts** page, choose **Create new prompt**\.

1. Choose the following actions:
   + **Upload**—Select the file to upload\.
   + **Record**—Select the red circle to begin recording\. Use the red square to stop\. You can choose **Crop** to cut the recorded prompt or **Discard** to record a new prompt\.

1. For **Step 2: Input basic information**, enter the name of the file, and then choose **Create**\.

**To manage recorded prompts**

1. In the navigation pane, choose **Routing**, **Prompts**\.

1. On the **Manage voice prompts** screen, select the appropriate prompt\.

1. You can choose **Play**, **Download**, **Edit**, or **Delete**\.

1. Choose **Save**\.

## Add Text\-to\-Speech<a name="text-to-speech"></a>

Amazon Connect supports text\-to\-speech, including SSML or plaintext with \(or without\) dynamic attributes\. You can enter text\-to\-speech prompts in any of the contact flow blocks that support prompt entry, such as **Play prompt** and **Get customer input**\. The text\-to\-speech voice is selected in the **Set voice** contact block\. You can also use SSML in Amazon Lex bots to modify the voice used by a chat bot when interacting with your customers\. For more information about using SSML in Amazon Lex bots, see [Managing Messages](https://docs.aws.amazon.com/lex/latest/dg//howitworks-manage-prompts.html#msg-prompts-response) and [Managing Conversation Context](https://docs.aws.amazon.com/lex/latest/dg//context-mgmt.html#special-response) in the Amazon Lex Developer Guide\.

Amazon Connect uses Amazon Polly, a service that converts text into lifelike speech using Speech Synthesis Markup Language \(SSML\)\. For more information, see [Using SSML](https://docs.aws.amazon.com/polly/latest/dg/ssml.html) in the Amazon Polly Developer Guide\.

SSML\-enhanced input text gives you more control over how Amazon Connect generates speech from the text you provide\. You can customize and control aspects of speech such as pronunciation, volume, and speed\. Amazon Polly provides this level of control using a subset of the SSML markup tags as defined by [Speech Synthesis Markup Language \(SSML\) Version 1\.1, W3C Recommendation](https://www.w3.org/TR/2010/REC-speech-synthesis11-20100907/)\.

### Modify a Prompt using SSML<a name="ssml-prompt"></a>

When you add a prompt to a contact flow, you can use SSML tags to provide a more personalized experience for your customers\. The default setting in a contact flow block for interpreting text to speech is **Text**\. To use SSML for text to speech in your contact flow blocks, set the **Interpret as** field to **SSML** as shown in the following image\.

![\[Image of the settings for a contact flow block showing the Text to speech Interpret as field set to SSML.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/connect-interpret-as-ssml.png)

The following SSML tags are supported in Amazon Connect:
+ speak
+ break
+ lang
+ mark
+ p
+ phoneme
+ prosody
+ s
+ say\-as
+ sub
+ w
+ amazon:effect name="whispered"

If you use an unsupported tag in your input text it is automatically ignored when it is processed\. To learn more about the SSML tags, see [SSML Tags in Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/supported-ssml.html)\.