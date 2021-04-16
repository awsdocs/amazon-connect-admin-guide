# Contact block: Set voice<a name="set-voice"></a>

## Description<a name="set-voice-description"></a>
+ Sets the text\-to\-speech \(TTS\) language and voice to use for the contact flow\.
+ The default voice is configured to Joanna \(Conversational speaking style\), an [Amazon Polly Neural Text\-to\-Speech \(NTTS\)](https://docs.aws.amazon.com/polly/latest/dg/NTTS-main.html) voice\. Neural voices make automated conversations sound more lifelike by improving the pitch, inflection, intonation, and tempo\.
+ After this block is run, any TTS invocation resolves to the neural or standard voice selected\.
+ If this block is triggered during a chat conversation, the contact goes down the **Success** branch\. It has no effect on the chat experience\. 

## Contact flow types<a name="set-voice-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ All flows

## Properties<a name="set-voice-properties"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-properties.png)

## Configuration tips<a name="set-voice-tips"></a>
+ For the **Joanna** and **Matthew** neural voices, in American English \(en\-US\), you can also specify a [Conversational speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html) or a [Newscaster speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html)\.

## Configured block<a name="set-voice-configured"></a>

When this block is configured, it looks similar to the following image:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/set-voice-configured.png)

## Scenarios<a name="set-voice-scenarios"></a>

See these topics for scenarios that use this block:
+ [Add text\-to\-speech to prompts](text-to-speech.md)