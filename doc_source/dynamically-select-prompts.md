# Dynamically select which prompts to play<a name="dynamically-select-prompts"></a>

You can dynamically select which prompt to play by using an attribute\.

1. Add [Set contact attributes](set-contact-attributes.md) blocks to your flow\. Configure each one to play the appropriate audio prompt\. For example, the first one might play the \.wav file when your contact center is open\. The second one might play the \.wav file for when it's closed\.

   The following image shows how you might configure a [Set contact attributes](set-contact-attributes.md) block\. In this example, the user\-defined attribute is named **CompanyWelcomeMessage**\. You can name your attribute anything you want\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties-2-a-new.png)

1. In the [Play prompt](play.md) block, choose **User Defined**, and then enter the name of the attribute that you created in step 1\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties2.png)

1. Connect the [Set contact attributes](set-contact-attributes.md) blocks to the **Play prompt** block\. The following example shows how it might look if you added one of each block to test how this works\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/play-prompt-properties-2-b.png)