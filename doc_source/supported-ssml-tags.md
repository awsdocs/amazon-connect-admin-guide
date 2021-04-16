# SSML tags supported by Amazon Connect<a name="supported-ssml-tags"></a>

Amazon Connect supports the following SSML tags\. To learn more about the SSML tags, see [Supported SSML Tags](https://docs.aws.amazon.com/polly/latest/dg/supportedtags.html) in the Amazon Polly Developer Guide\.

**Tip**  
If you use an unsupported tag in your input text, it's automatically ignored when it's processed\. 


| Tag | Use to\.\.\. | 
| --- | --- | 
|  speak  |  All SSML\-enhanced text must be enclosed within a pair of speak tags\.  | 
|  break  |  Add a pause to your text\. The maximum duration for a pause is 10 seconds\.  | 
|  lang  |  Specify another language for specific words\.  | 
|  mark  |  Put a custom tag within the text\.  | 
|  p  |  Add a pause between paragraphs in your text\.   | 
| phoneme | Make a phonetic pronunciation for specific text\. | 
| prosody | Control the volume, rate, or pitch of your selected voice\. | 
| s | Add a pause between lines or sentences in your text\. | 
| say\-as | Combine with the interpret\-as attribute to tell Amazon Polly how to say certain characters, words, and numbers\. | 
| sub | Combine with the alias attribute to substitute a different word \(or pronunciation\) for selected text such as an acronym or abbreviation\. | 
| w | Customize the pronunciation of words by specifying the word’s part of speech or alternate meaning\. | 
| amazon:effect name="whispered"  | Indicate that the input text should be spoken in a whispered voice rather than as normal speech\. | 

If you use an unsupported tag in your input text it is automatically ignored when it is processed\. 

To learn more about the SSML tags, see [SSML Tags Supported by Amazon Polly](https://docs.aws.amazon.com/polly/latest/dg/supported-ssml.html)\.

## Neural and Conversational Speaking Styles<a name="neural-and-conversational-tts"></a>

For the **Joanna** and **Matthew** neural voices, in American English \(en\-US\), you can also specify a [Conversational speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html) or a [Newscaster speaking style](https://docs.aws.amazon.com/polly/latest/dg/ntts-speakingstyles.html)\.