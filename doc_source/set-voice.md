# Contact block: Set voice<a name="set-voice"></a>

## Description<a name="set-voice-description"></a>
+ Sets the text\-to\-speech \(TTS\) language and voice to use for the contact flow\.
+ The default voice is configured to Joanna \(Conversational speaking style\)\. 
+ You can choose **Override speaking style** to make it and other voices [Amazon Polly Neural Text\-to\-Speech \(NTTS\)](https://docs.aws.amazon.com/polly/latest/dg/NTTS-main.html)\. Neural voices make automated conversations sound more lifelike by improving the pitch, inflection, intonation, and tempo\.

  For a list of supported neural voices, see [Neural Voices](https://docs.aws.amazon.com/polly/latest/dg/ntts-voices-main.html) in the *Amazon Polly Developer Guide*\. 
+ After this block is run, any TTS invocation resolves to the neural or standard voice selected\.
+ If this block is triggered during a chat conversation, the contact goes down the **Success** branch\. It has no effect on the chat experience\. 

## Supported channels<a name="set-voice-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | No \- Success branch | 
| Task | No \- Success branch | 

## Contact flow types<a name="set-voice-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="set-voice-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-properties.png)

**Tip**  
For voices that support only neural speaking styles but not standard, the **Override speaking style** is automatically selected\. You do not have the option to unselect it\.

## Use an Amazon Lex V2 bot with Amazon Connect<a name="set-voice-lexv2bot"></a>

If you're using an Amazon Lex V2 bot, your language attribute in Amazon Connect must match the language model used to build your Lex bot\. This is different than Amazon Lex \(Classic\)\. 
+ If you build an Amazon Lex V2 bot with a different language model—for example, en\_AU, fr\_FR, es\_ES, and more—under **Voice**, choose a voice that corresponds to that language, and then must choose **Set language attribute**, as shown in the following image\.
+ If you're not using an en\-US voice with an Amazon Lex V2 bot and don't choose **Set language attribute**, the [Get customer input](get-customer-input.md) block results in an error\.
+ For bots with multiple languages \(for example, en\_AU and en\_GB\) choose **Set language attribute** for one of the languages\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-properties3.png)

## Configuration tips<a name="set-voice-tips"></a>
+ For the **Joanna** and **Matthew** neural voices, in American English \(en\-US\), you can also specify a [Conversational speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html) or a [Newscaster speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html)\.

## Configured block<a name="set-voice-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-configured.png)

## Scenarios<a name="set-voice-scenarios"></a>

See these topics for scenarios that use this block:
+ [Add text\-to\-speech to prompts](text-to-speech.md)