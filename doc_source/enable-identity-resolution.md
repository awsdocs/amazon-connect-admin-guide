# Enable Identity Resolution for your Customer Profiles domain<a name="enable-identity-resolution"></a>

When you enable Identity Resolution you specify the following information:
+ When the Identity Resolution Job should run on a weekly basis\. By default, it runs Saturdays at 12AM UTC\.
+ The Amazon S3 bucket where the Identity Resolution Job should write the results of the automatic profile matching process\. If you don't have an S3 bucket, you'll have the option to create one during the enablement process\. 

  You can query the Amazon S3 bucket or use the [GetMatches](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetMatches.html) API to filter results based on [confidence scores](how-identity-resolution-works.md#confidence-score)\.

**Note**  
After you enable Identity Resolution you'll see the option to [create consolidation criteria](create-consolidation-criteria.md) for the optional auto\-merging process\.

**To enable Identity Resolution**

1. You must have a Customer Profiles domain enabled for your instance\. For instructions, see [Enable Customer Profiles for your instance](enable-customer-profiles.md)\.

1. In the navigation pane, choose **Customer profiles**\.

1. In the **Identity Resolution** section, choose **Enable Identity Resolution**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-enable-ir.png)

1. On the **Enable Identity Resolution** page, specify the date and time when you want the Identity Resolution Job to run\.

1. If you want to review the matched profile IDs from an Amazon S3 bucket, select **Write profile ID matches to Amazon S3**\. Otherwise, you can use the [GetMatches](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_GetMatches.html) API to review matching profiles\. 

   1. Specify the Amazon S3 bucket where the Identity Resolution Job should write the profile matches\.

     We recommend applying a policy to prevent a confused deputy security issue\. For more information and a sample policy, see [Amazon Connect Customer Profiles cross\-service confused deputy prevention](cross-service-confused-deputy-prevention.md#customer-profiles-cross-service)\.

1. When done, choose **Enable Identity Resolution**\.

1. After you enable Identity Resolution the Identity Resolution Job runs for the first time within 24 hours\.
**Note**  
Before running an Identity Resolution Job for the first time on a new Customer Profiles domain, we recommend checking your profile metrics to make sure that profiles have been created\. Otherwise, there won't be any matching results\.

1. You may want to set up consolidation criteria for auto\-merging matching profiles\. If so, see [Set up consolidation criteria for Identity Resolution](create-consolidation-criteria.md)\.