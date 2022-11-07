# Delete traffic distribution groups<a name="delete-traffic-distribution-groups"></a>

Use the [DeleteTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DeleteTrafficDistributionGroup.html) API to delete a traffic distribution group that is no longer needed\.

**Note**  
You cannot delete a traffic distribution group if phone numbers are claimed to it\. You must first release phone numbers from the traffic distribution group by using the [ReleasePhoneNumber](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReleasePhoneNumber.html) API\. After that, you can delete the traffic distribution group\.  
You cannot release numbers from a traffic distribution group by using the Amazon Connect console\. 

Your [DeleteTrafficDistributionGroup](https://docs.aws.amazon.com/connect/latest/APIReference/API_DeleteTrafficDistributionGroup.html) API call will fail with an `ResourceInUseException` if phone numbers are still claimed to the traffic distribution group\.