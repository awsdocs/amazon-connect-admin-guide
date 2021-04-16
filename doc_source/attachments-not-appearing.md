# Attachments are not appearing in chats<a name="attachments-not-appearing"></a>

The following issues may cause attachments to not display for your agents using chat\. 

## Internal firewall settings are preventing access<a name="update-firewall-settings"></a>

 Check that your firewall isn't preventing agents from accessing the files in your Amazon S3 bucket\. You may need to add the Amazon S3 bucket where your files are stored to your domain allow list\. For more information, see [Set up your network](ccp-networking.md)\. 

## Attachments are too large, too many, or don't meet file type requirements<a name="check-attachment-size"></a>

Check that the attachments meet the size, number, and file type requirements\. For more information, see [Feature specifications](amazon-connect-service-limits.md#feature-limits)\.

To calculate the size of an attachment \(artifactSizeInBytes\), use a third\-party tool such as [ File\.size](https://developer.mozilla.org/en-US/docs/Web/API/File/size)\.