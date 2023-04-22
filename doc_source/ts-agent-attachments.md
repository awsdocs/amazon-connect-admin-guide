# Internal firewall prevents access to chat attachments<a name="ts-agent-attachments"></a>

This topic is for developers who need to investigate issues that may occur when using the chat channel in Amazon Connect\.

The following issues, setting as internal firewall settings, may cause attachments to not display for your agents using Amazon Connect chat\. 

## Internal firewall settings are preventing access<a name="update-firewall-settings"></a>

 Check that your firewall isn't preventing agents from accessing the files in your Amazon S3 bucket\. You may need to add the Amazon S3 bucket where your files are stored to your domain allow list\. For more information, see [Set up your network](ccp-networking.md)\. 

## Attachments are too large, too many, or don't meet file type requirements<a name="check-attachment-size"></a>

Check that the attachments meet the size, number, and file type requirements\. For more information, see [Amazon Connect feature specifications](feature-limits.md)\.

To calculate the size of an attachment \(artifactSizeInBytes\), use a third\-party tool such as [ File\.size](https://developer.mozilla.org/en-US/docs/Web/API/File/size)\.