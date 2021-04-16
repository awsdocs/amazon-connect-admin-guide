# Contact block: Play prompt<a name="play"></a>

## Description<a name="play-description"></a>
+ This block can play an interruptible audio prompt, play a text\-to\-speech message, or send a chat response\.
+ Amazon Connect includes a set of pre\-recorded prompts for you to use\. However, you can record and upload your audio prompts\. For instructions, see [Create prompts](prompts.md)\.

## Contact flow types<a name="play-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound contact flow
+ Customer Queue flow
+ Customer Whisper flow
+ Agent Whisper flow
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="play-properties"></a>

The properties give you different ways to choose the prompt to be played:
+ **Select from the prompt library \(audio\)**: Choose from one of the pre\-recorded prompts included with Amazon Connect, or [record and upload](prompts.md) your own prompt\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties1.png)
+ **Select dynamically**: 

  You can select which prompt to play by using an attribute\.

  1. Add [Set contact attributes](set-contact-attributes.md) blocks to your flow\. Configure each one to play the appropriate audio prompt\. For example, the first one might play the \.wav file for when your contact center is open\. The second one might play the \.wav file for when it's closed\.

     The following image shows how you might configure a [Set contact attributes](set-contact-attributes.md) block\. In this example, the user\-defined attribute is named **CompanyWelcomeMessage**\. You can name your attribute anything you want\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties-2-a-new.png)

  1. In the [Play prompt](#play) block, choose **User Defined**, and then enter the name of the attribute that you created in step 1\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties2.png)

  1. Connect the [Set contact attributes](set-contact-attributes.md) blocks to the **Play prompt** block\. The following example shows how it might look if you added one of each block to test how this works\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties-2-b.png)

  In a real life scenario, you would have multiple [Set contact attributes](set-contact-attributes.md)\. Each instance of CompanyWelcomeMessage would be set to a different ARN, depending on the scenario\. For example, you might start with a [Check hours of operation](check-hours-of-operation.md) block\. If your call center is closed, the flow branches to one **Set contact attributes** block\. If it's open, the flow branches to another\.
+ **Text\-to\-speech or chat text**: You have two options: 
  + **Enter text**: To play text, Amazon Connect sends it to Amazon Polly, a service that converts text into lifelike speech using Speech Synthesis Markup Language \(SSML\)\. Amazon Polly returns the speech to Amazon Connect to play\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties3.png)
  + **Enter dynamically**: Upload \.wav files that should be played, based on the value of the attribute\.
+ **Interpret as**: The default setting in a contact flow block for interpreting text\-to\-speech is Text\. To use SSML for text\-to\-speech in your contact flow blocks, set the **Interpret as** field to **SSML** as shown in the following image\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties4.png)

  When you add a prompt to a contact flow, you can use SSML tags to provide a more personalized experience for your customers\. SSML tags are a way to control how Amazon Polly generates speech from the text you provide\.

  To learn which SSML tags Amazon Connect supports, see [SSML tags supported by Amazon Connect](supported-ssml-tags.md)\. 

## Configuration tips<a name="play-tips"></a>

When you use text, either for text\-to\-speech or chat, you can use a maximum of 3,000 billed characters \(6,000 total characters\)\. You can also specify text in a flow using a contact attribute\.

## Configured block<a name="play-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-configured.png)

## Sample flows<a name="play-samples"></a>

All of the sample flows use the **Play prompt** block\. Take a look at the [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md) to see a **Play prompt** for chat and one for audio\.