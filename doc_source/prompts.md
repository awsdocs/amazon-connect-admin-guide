# Create prompts<a name="prompts"></a>

Prompts are audio files played in call flows\. For example, hold music is a prompt\. Amazon Connect comes with a set of prompts that you can add to your contact flows\. Or, you can add your own recordings\. 

We recommend that you align your prompts and routing policies with each other to ensure a smooth call flow for customers\.

**To create a prompt**

1. In the navigation pane, choose **Routing**, **Prompts**\.

1. On the **Manage voice prompts** page, choose **Create new prompt**\.

1. Choose the following actions:
   + **Upload**—Select the file to upload\.
   + **Record**—Select the red circle to begin recording\. Use the red square to stop\. You can choose **Crop** to cut the recorded prompt or **Discard** to record a new prompt\.

1. For **Step 2: Input basic information**, enter the name of the file, and then choose **Create**\.

## Supported file types<a name="supported-file-types-for-prompts"></a>

You can upload a pre\-recorded \.wav file to use for your prompt, or record one in the web application\.

We recommend using 8 KHz \.wav files that are less than 50 MB and less than 5 minutes long\. If you use higher rated audio libraries, such as 16 KHz or 16 bit files, Amazon Connect has to down sample them into 8 KHz samples because of PSTN limitations\. This may result in low quality audio\. For more information, see the following Wikipedia article: [G\.711](https://en.wikipedia.org/wiki/G.711)\. 

## Maximum length for prompts<a name="max-length-for-prompts"></a>

Amazon Connect supports prompts that are less than 50 MB and less than 5 minutes long\. 

## Bulk upload of prompts not supported in UI, API, or CLI<a name="bulk-upload-prompts"></a>

Currently, bulk uploading of prompts is not supported through the Amazon Connect console or programmatically using the API or CLI\.