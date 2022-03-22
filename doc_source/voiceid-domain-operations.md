# Voice ID domain operations<a name="voiceid-domain-operations"></a>

Amazon Connect Voice ID provides APIs for you manage Voice ID domains\. You can find equivalents for Create, Update, Describe and List in the AWS Console\.

1. [CreateDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_CreateDomain.html): To create a new Voice ID domain, you can use the `CreateDomain` Voice ID API\. You can only invoke this for your account after you have acknowledged the BIPA Consent in the AWS console\. You must also specify the KMS key for the Voice ID domain at the time of creation\. 

   Creating a domain doesn't associate it with a Amazon Connect instance\. You must call the [Amazon Connect association APIs](https://docs.aws.amazon.com/connect/latest/APIReference/) to do so\.

1.  [UpdateDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_UpdateDomain.html): To update the name and encryption configuration for a domain, you can use the `UpdateDomain` Voice ID API\. This API clobbers existing attributes, and you must provide both these fields\. 

    When you update/change the KMS key associated with the Voice ID domain that is being used for enrollments and authentication, any new enrollments that happen after the change use the new KMS key while the old ones continue to use the existing KMS key\. Voice ID does not re\-encrypt any of the existing enrollments with the new KMS key, and hence you need to retain your old KMS key and permissions to access the older key as well\.

1. [DescribeDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeDomain.html): Use this API to return the name, description and encryption configuration of an existing domain identified by its DomainID\.

1. [ListDomains](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListDomains.html): Use this API to list all your Voice ID domains owned by your account in the Region\.

1.  [DeleteDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteDomain.html): To delete a Voice ID domain, you must invoke the `DeleteDomain` Voice ID API and provide the domain ID\. If this domain was associated with a Amazon Connect instance, Voice ID API calls and Voice ID contact flow blocks will return runtime error\. Deleting a Voice ID domain deletes all stored customer data such as audio recordings, voiceprints and speaker identifiers, as well as fraudster lists that you managed\. 