# Evaluate performance \(Preview\)<a name="evaluations"></a>


|  | 
| --- |
| This feature is in preview release and subject to change\.  | 

Amazon Connect helps you to assess, track, and improve how agents interact with customers and resolve issues\. For example, you can search for a contact, choose the appropriate evaluation form, review the contact audio, transcript, or both, and then evaluate how the agent interacted with the customer\. You can then use that feedback to help the agent deliver improved customer experiences\.

**Tip**  
**IT administrators**: To enable the evaluations feature, go to the Amazon Connect console, choose your instance alias, choose **Data storage**, **Content evaluations**, **Edit**\. You'll be prompted to create or choose an S3 bucket\. After the bucket is created, you can store evaluations and export them\.

**To evaluate performance**

1. Log in to Amazon Connect with a user account that has [permissions to perform evaluations](evaluation-forms-permissions.md)\. 

1. Access the contact that you want to evaluate\. There are a few ways you can do this\. For example, someone may have shared the contact URL with you, or assigned you a task that has the URL\. Or, you may have the contact ID, which lets you search for the contact record by doing the following: on the navigation pane, choose **Analytics and optimization**, **Contact search**, and then search for the contact that you want to evaluate\.

1. On the **Contact details** page, choose **Evaluations** or the **<** icon\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-evaluatebutton.png)

1. The evaluations pane lists any evaluations that are in progress or completed for the contact\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-startevaluation.png)

1. To start an evaluation, choose an evaluation from the dropdown menu, and then choose **Start evaluation**\.

1. To navigate an especially long evaluation form, use the arrows next to each section to collapse or expand it\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-exampleevaluation.png)

1. Choose **Save** to save a form in progress\. The status of the form becomes **Draft**\. You can return to it any time to continue, or you can delete it and start over\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-draft.png)

1. When you're done, choose **Submit**\. The status of the form is **Completed**\.