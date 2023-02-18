# Create an evaluation form \(Preview\)<a name="create-evaluation-forms"></a>


|  | 
| --- |
| This feature is in preview release and subject to change\.  | 

In Amazon Connect, you can create [many different evaluation forms](feature-limits.md#evaluationforms-feature-specs)\. For example, you may need a different evaluation form for each business unit and type of interaction\. Each form can contain multiple sections and questions, and you can weigh how they factor into the agent's total score\.

This topic explains how to add sections and questions, assign weights for scoring, and then activate the evaluation form so that it is available to managers, for example, when they want to evaluate contacts\.

## Step 1: Assign a title to the form<a name="step-title"></a>

In this step, you assign a title to the form\. Evaluators will see this title in a dropdown menu\.

1. Log in to Amazon Connect with a user account that has [permissions to create evaluation forms](evaluation-forms-permissions.md)\. 

1. In Amazon Connect, choose **Analytics and optimization**, **Evaluation forms**\. 

1. On the **Evaluation forms** page, choose **Create new form**\. 

1. Assign a title for the form, for example, **Sales evaluation**\. Choose **Ok**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-title.png)

1. At the top of the evaluation form page, there are two tabs:
   + **Sections and questions**\. Add sections, questions, and answers to the form\.
   + **Scoring**\. Enable scoring on the form\. You can also apply scoring to sections or questions\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-enablescoringform2.png)

1. Choose **Save** at any time while creating your form\. This enables you to navigate away from the page and return to the form later\.

1. Continue to the next step to add sections and questions\.

## Step 2: Add sections and questions<a name="step-sections"></a>

1. While on the **Sections and questions** tab, add a title to the section 1, for example, **Greeting**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-greetingtitle.png)

1. Choose **Add question** to add a question\. 

1. In the **Question title** box, enter the question that will appear on the evaluation form\. For example, **Did the agent state their name and say they are here to assist?**   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-greetingquestion1.png)

1. In the **Instructions to evaluators** box, add information to help the evaluators answer the question, such as a link to an internal wiki or other resource\. 

1. In the **Question type** box, choose one of the following options to appear on the form:
   + **Single selection**: The evaluator can choose from a list of options, such as **Yes**, **No**, or **Good**, **Fair**, **Poor**\.
   + **Text field**: The evaluator can enter free form text\. 
   + **Number**: The evaluator can enter a number from a range that you specify, such as 1\-10\. 

1. Continue to the next step to add answers\.

## Step 3: Add answers<a name="step-answers"></a>

1. On the **Answers** tab, add answer options that you want to display to evaluators, such as **Yes**, **No**\.

1. To add more answers, choose **Add option**\. 

   The following image shows example answers for a **Single selection** question\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-greetingquestion1-answer.png)

   The following image shows an answer range for a **Number** question\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-questionscoring4.png)

1. When you're finished adding answers, continue to the next step to enable scoring, and add ranges for scoring **Number** answers\. 

## Step 4: Assign scores and ranges to answers<a name="step-assignscores"></a>

1. Go to the top of the form\. Choose the **Scoring** tab, and then choose **Enable scoring**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-enablescoring.png)

   This enables scoring for the entire form\. It also enables you to add ranges for answers to **Number** question types\.

1. Return to the **Sections and questions** tab\. Now you have the option to assign scores to **Single selection**, and add ranges for **Number** question types\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-scoring-feature.png)

1. When you create a **Number** type question, on the **Scoring** tab, choose **Add range** to enter a range of values\. Indicate the worst to best score for the answer\. 

   The following image shows an example of ranges and scoring for a **Number** question type\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-questionscoring5.png)
   + If the agent interrupted the customer 0 times, they get a score of 10 \(best\)\.
   + If the agent interrupted the customer 1\-4 times, they get a score of 5\. 
   + If the agent interrupted the customer 5\-10 times, they get a score of 1 \(worst\)\. 

1. After you assign scores to all the answers, choose **Save**\.

1. When you're finished assigning scores, continue to the next step to automate the question of certain questions, or continue to [preview the evaluation form](#step-preview)\. 

## Step 5: Enable automated evaluations<a name="step-automate"></a>

Contact Lens lets you to define agent performance criteria \(for example, adherence to required scripts\), and then use that criteria to automatically complete evaluation forms\. You set up the criteria and logic for each question where you want to allow automated evaluations\. 

Following are examples of setting up automated evaluations, one for a Single section question and another for a Numeric question\.

**Example automation for a Single selection question**
+ If the agent mentioned X or Y in the script, score this question as Yes\. 

  The following image shows that when Contact Lens detects the words or phrases in the **ScriptCompliance** category, the question will automatically be answered **Yes**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-automation1.png)

   For information about setting up the criteria, see [Automatically categorize contacts based on uttered keywords and phrases](rules.md)\.

**Example automation for a Numeric question**
+ If the agent interaction duration was less than 30 seconds, score the question as a 10\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-automation2.png)
+ On the **Automation** tab, choose the metric that is used to automatically evaluate the question\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-automation3.png)
+ You can use any metadata that is a number\. For example, first response time, sentiment score, and non\-talk time\. 

## Step 6: Preview the evaluation form<a name="step-preview"></a>

The **Preview** button is active only after you have assigned scores to answers for all of the questions\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-previewbutton.png)

The following image shows the form preview\. Use the arrows to collapse sections and make the form easier to preview\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-previewmode.png)

## Step 7: Assign weights for final score<a name="step-weights"></a>

When scoring is enabled for the evaluation form, you can assign *weights* to sections or questions\. The weight raises or lowers the impact of a section or question on the final score of the evaluation\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-scoring.png)

### Weight distribution mode<a name="weight-distribution-mode"></a>

With **Weight distribution mode**, you choose whether to assign weight by section or question: 
+ **Weight by section**: You can evenly distribute the weight of each question in the section\.
+ **Weight by question**: You can lower or raise the weight of specific questions\.

When you change a weight of a section or question, the other weights are automatically adjusted so the total is always 100 percent\.

For example, in the following image, three of the questions were manually set to 10 percent\. The weights that display in italics were adjusted automatically\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/evaluationforms-weightdistribution2.png)

## Step 8: Activate an evaluation form<a name="step-activateform"></a>

Choose **Activate** to make the form available to evaluators\. Evaluators will no longer be able to choose the previous version of the form from the dropdown list\.

Previous versions of the form are linked to the completed evaluations based on them\. This allows you to view the version of the form that the evaluation is based on\.