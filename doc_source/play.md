# Flow block: Play prompt<a name="play"></a>

## Description<a name="play-description"></a>
+ This block can play an interruptible audio prompt, play a text\-to\-speech message, or send a chat response\.
+ Amazon Connect includes a set of pre\-recorded prompts for you to use\.
+ To use your own voice prompts, you have the following options:
  + **Use the Amazon Connect library**: You can record and upload your audio prompts in using the Amazon Connect admin console\. For instructions, see [Create prompts](prompts.md)\.
  + **Use Amazon S3**: You can store as many voice prompts as needed in Amazon S3 and access them in real time by using contact attributes in the **Play prompt** block\. 

    For example, based on a customer's preferred language, you can dynamically play a voice prompt with a local accent that greets them and thanks them for being a loyal member\. You can even concatenate multiple attributes, such as line of business or language preference to create personalized interactions; for example, reservations \+ Spanish language\.

## Requirements<a name="requirements"></a>
+ **Supported formats**: Amazon Connect supports \.wav files to use for your prompt\. You must use \.wav files that are 8KHz, and mono channel audio with U\-Law encoding\. Otherwise, the prompt won't play correctly\. You can use publicly available third\-party tools to convert your \.wav files to U\-Law encoding\. After converting the files, upload them to Amazon Connect\.
+ **Size**: Amazon Connect supports prompts that are less than 50MB and less than five minutes long\.
+ **When storing prompts in an S3 bucket:** For Regions that are disabled by default \(also called [opt\-in](https://docs.aws.amazon.com/general/latest/gr/rande-manage.html) Regions\) such as Africa \(Cape Town\), your bucket must be in the same Region\.

## Supported channels<a name="play-channels"></a>

The following table lists how this block routes a contact who is using the specified channel\. 


| Channel | Supported? | 
| --- | --- | 
| Voice | Yes | 
| Chat | Yes | 
| Task | No \- takes the **Okay** branch but it has no effect | 

## Flow types<a name="play-types"></a>

You can use this block in the following [contact flow types](create-contact-flow.md#contact-flow-types):
+ Inbound flow
+ Customer Queue flow
+ Customer Whisper flow\. You can play prompts from the Amazon Connect library but not prompts stored in Amazon S3\. 
+ Agent Whisper flow: You can play prompts from the Amazon Connect library but not prompts stored in Amazon S3\. 
+ Transfer to Agent flow
+ Transfer to Queue flow

## Properties<a name="play-properties"></a>

The properties provide you different ways to choose the prompt to be played\.

### Prompts stored in library<a name="play-properties-library"></a>

**Select from the prompt library \(audio\)**: Choose from one of the pre\-recorded prompts included with Amazon Connect, or use the Amazon Connect admin console to [record and upload](prompts.md) your own prompt\. There's no way to upload prompts in bulk\.

The following image shows the **Properties** page of the **Play prompt** block configured to play an Audio prompt from the prompt library\.

![\[The properties page of the Play prompt block, prompt library.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/playprompt-properties-library-manually.png)

### Prompts stored in Amazon S3<a name="play-properties-s3"></a>

**Specify an audio file from an S3 bucket**: Store as many prompts as you need in an S3 bucket and then refer to them by specifying the bucket path\. For best performance, we recommend creating the S3 bucket in the same Region as your Amazon Connect instance\.

The following image shows the **Properties** page of the **Play prompt** block configured to set the S3 file path manually\.

![\[The properties page of the Play prompt block, S3 file path specified manually.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/playprompt-properties-s3-manually.png)

The following image shows how to specify the S3 bucket path using attributes:

![\[The S3 file path specified manually using attributes.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/playprompt-properties-s3-jsonpath.png)

You can provide the S3 path with concatenation, as shown in the following example\. This enables you to personalize the prompt, for example, by line of business and language\. 

Note that only the last part of path is shown in the image but you would enter the full path, for example:

`https://example.s3.amazon.aws.com/$['Attributes']['Language']/$['Attributes']['LOB']/1.wav`

![\[The last part of the S3 file path.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/playprompt-properties-s3-concatentation.png)

The following example shows how you can specify the S3 path dynamically using a user\-defined attribute named **S3filepath**\.

![\[The S3 file path set dynamically, the namespace set to User-defined.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/playprompt-properties-s3-attributes.png)

### Text\-to\-speech or chat text<a name="play-properties-text-to-speech"></a>

You can enter a prompt in plain text, or SSML, as shown in the following image:

![\[A text-to-speech prompt set manually.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-sample-ssml.png)

SSML\-enhanced input text gives you more control over how Amazon Connect generates speech from the text you provide\. You can customize and control aspects of speech such as pronunciation, volume, and speed\.

For a list of SSML tags you can use with Amazon Connect, see [SSML tags supported by Amazon Connect](supported-ssml-tags.md)\. 

For more information, see [Add text\-to\-speech to prompts](text-to-speech.md)\.

## Configuration tips<a name="play-tips"></a>
+ For step\-by\-step instructions about how to set up a dynamic prompt using contact attributes, see [Dynamically select which prompts to play](dynamically-select-prompts.md)\.
+ When playing prompts from an S3 bucket, for best performance we recommend creating the bucket in the same Region as your Amazon Connect instance\.
+ When you use text, either for text\-to\-speech or chat, you can use a maximum of 3,000 billed characters, which is 6,000 characters total\. You can also specify text in a flow using a contact attribute\.
+ Some existing flows have a version of the **Play prompt** block that doesn't have an **Error** branch\. In this case, the **Okay** branch will always be taken at runtime\. If you update the configuration of a **Play prompt** block that doesn't have an **Error** branch, an **Error** branch will be added to the block automatically in the editor\.
+ A contact is routed down the **Error** branch in the following situations:
  + Amazon Connect is unable to download the prompt from S3\. This may be due to an incorrect file path, or the S3 bucket policy is not set up correctly and Amazon Connect does not have access\. For instructions about how to apply the policy, and a template you can use, see [Set up prompts to play from an S3 bucket](setup-prompts-s3.md)\.
  + Incorrect audio file format\. Only \.wav files are supported\.
  + The audio file is larger than 50MB or longer than five minutes\.
  + The SSML is incorrect\. 
  + The text\-to\-speech length exceeds 6000 characters\. 
  + The the Amazon Resource Name \(ARN\) for the prompt is incorrect\.

## Configured block<a name="play-configured"></a>

The following image shows what a Play prompt block looks like when it's configured for text\-to\-speech\. It shows the text to be played, and it has two branches: **Success** and **Error**\.

![\[A Play prompt block configured for text-to-speech.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-configured.png)

The following image shows what this block looks like when it's configured for an S3 bucket\. It shows the S3 path, and it has two branches:**Success** and **Error**\.

![\[A Play prompt block configured for an S3 path.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-configured2.png)

## Sample flows<a name="play-samples"></a>

All of the sample flows use the **Play prompt** block\. Take a look at the [Sample inbound flow \(first contact experience\)](sample-inbound-flow.md) to see a **Play prompt** for chat and one for audio\.