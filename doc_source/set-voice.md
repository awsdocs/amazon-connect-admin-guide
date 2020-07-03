# Contact Block: Set Voice<a name="set-voice"></a>

## Contact flow types<a name="set-voice-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Description<a name="set-voice-description"></a>
+ Sets the text\-to\-speech \(TTS\) language and voice to use for the contact flow\.
+ The default voice is configured to Joanna, an [Amazon Polly Neural Text\-to\-Speech \(NTTS\)](https://docs.aws.amazon.com/polly/latest/dg/NTTS-main.html) voice\. Neural voices make automated conversations sound more lifelike by improving the pitch, inflection, intonation, and tempo\.
+ After this block is run, any TTS invocation resolves to the neural or standard voice selected\.
+ If this block is triggered during a chat conversation, the contact goes down the **Success** branch but the block has no impact\.

## Properties<a name="set-voice-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-properties.png)

## Configuration tips<a name="set-voice-tips"></a>
+ For the **Joanna** and **Matthew** neural voices, in American English \(en\-US\), you can also specify a [Conversational speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html) or a [Newscaster speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html)\.
+ To enable a speaking style, in the blocks where you include text\-to\-speech \(that is, [Play Prompt](play.md), [Get Customer Input](get-customer-input.md), and [Store Customer Input](store-customer-input.md)\), perform the following steps:

  1. Add the appropriate SSML tags to the text\. For example, the following image shows how to specify the Conversational speaking style:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-tts-example.png)

  1. In the **Interpret as** drop\-down box, choose **SSML**\. The following image shows where this option is in the properties for the **Play prompt** block:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-tts-example2.png)
**Important**  
Don't use SSML tags for a chat conversation\. The tags will appear in the chat window\.
+ To specify the Newscaster speaking style, enter **news** for the domain name instead of **conversational**\.
+ Add these SSML tags each time you invoke TTS, whether for Amazon Connect or Amazon Lex\.

## Configured block<a name="set-voice-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-configured.png)

## Scenarios<a name="set-voice-scenarios"></a>

See these topics for scenarios that use this block:
+ [Add text\-to\-speech to prompts](text-to-speech.md)