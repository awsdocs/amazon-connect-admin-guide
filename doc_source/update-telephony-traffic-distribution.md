# Update telephony traffic distribution across AWS Regions<a name="update-telephony-traffic-distribution"></a>

After you have claimed phone numbers to your traffic distribution group, use the [UpdateTrafficDistribution](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateTrafficDistribution.html) API to distribute telephony traffic across linked instances in a given traffic distribution group in 10% increments\. 

## Requirements<a name="update-telephony-traffic-distribution-requirements"></a>

If the following requirements are not met, your [UpdateTrafficDistribution](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateTrafficDistribution.html) API call will fail with an `InvalidRequestException`:
+ You must provide distribution for telephony traffic configuration\.
+ You must specify the traffic distribution for both linked instances and the total distribution must add up to 100%\.
+ You must specify traffic distribution in 10% increments\.
+ The instance ARNs specified in the telephony configuration must match the ARNs of the linked instances\.