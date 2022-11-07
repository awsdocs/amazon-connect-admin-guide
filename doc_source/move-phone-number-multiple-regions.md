# Move a claimed phone number to multiple instances across AWS Regions<a name="move-phone-number-multiple-regions"></a>

**Note**  
This feature is available only for Amazon Connect instances created in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.   
To obtain access to this feature, contact your Amazon Connect Solutions Architect or Technical Account Manager\.

You can move a phone number that was previously claimed to an instance, and instead assign it to multiple instances across AWS Regions\. You do this by assigning the phone number to a traffic distribution group\.

**To assign a phone number to a traffic distribution group**

1. Create a traffic distribution group using the [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API\.

1.  Describe your traffic distribution group using the [DescribeTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeTrafficDistributionGroup.html) API to determine whether it has been created successfully \(`Status` must be `ACTIVE`\)\.

1. After your traffic distribution group is created successfully \(`Status` is `ACTIVE`\), you can assign phone numbers that were previously claimed to other instances or other traffic distribution groups\. Use the [UpdatePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdatePhoneNumber.html) API\. 