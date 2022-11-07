# Claim phone numbers to instances across multiple AWS Regions<a name="claim-phone-number-multiple-regions"></a>

**Note**  
This feature is available only for Amazon Connect instances created in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.   
To obtain access to this feature, contact your Amazon Connect Solutions Architect or Technical Account Manager\.

To place or receive calls to a phone number across instances in multiple AWS Regions, you need to claim a phone number to a traffic distribution group\. 

**To claim a phone number to a traffic distribution group**

1. Create a traffic distribution group by using the [CreateTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateTrafficDistributionGroup.html) API\.

1. Describe your traffic distribution group by using the [DescribeTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DescribeTrafficDistributionGroup.html) API to determine whether it has been created successfully \(`Status` must be `ACTIVE`\)\.

1. After your traffic distribution group has been created successfully \(`Status` is `ACTIVE`\), you can claim phone numbers to it by using the [ClaimPhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ClaimPhoneNumber.html) API\. 