# Voice ID domain operations<a name="voiceid-domain-operations"></a>

Amazon Connect Voice ID provides APIs for you manage Voice ID domains\. You can find equivalents for Create, Describe, List, and Update in the AWS Console\.

1. [CreateDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_CreateDomain.html): To create a new Voice ID domain, use the `CreateDomain` Voice ID API\. When the Voice ID domain is created, a default fraudster watchlist to hold your fraudsters is created at the same time\.

   Note the following guidelines when using the `CreateDomain` API:
   +  You can only invoke this for your account after you have acknowledged the BIPA Consent in the AWS console\. 
   +  You must also specify the KMS key for the Voice ID domain at the time of creation\.
   + After creating a Voice ID domain, use the [Amazon Connect association APIs](https://docs.aws.amazon.com/connect/latest/APIReference/) to associate it with an Amazon Connect instance\.

1.  [DeleteDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteDomain.html): To delete a Voice ID domain, you must invoke the `DeleteDomain` Voice ID API and provide the domain ID\. If this domain was associated with an Amazon Connect instance, Voice ID API calls, and Voice ID flow blocks will return runtime error\. Deleting a Voice ID domain deletes all stored customer data such as audio recordings, voiceprints and speaker identifiers, as well as fraudster lists that you managed\. 

1. [DescribeDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeDomain.html): Use this API to return the name, description and encryption configuration of an existing domain identified by its `DomainID`\.

1. [ListDomains](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListDomains.html): Use this API to list all your Voice ID domains owned by your account in the Region\.

1.  [UpdateDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_UpdateDomain.html): To update the name and encryption configuration for a domain, you can use the `UpdateDomain` Voice ID API\. This API clobbers existing attributes, and you must provide both these fields\. 

   When you change the KMS key associated with the Voice ID domain, following the `UpdateDomain` call your domain's existing data will be asynchronously re\-encrypted under the new KMS key\. You can check status of this process from your domain's `ServerSideEncryptionUpdateDetails` attribute using the `DescribeDomain` API\. While this update process is in progress, you must retain your old KMS key in an accessible state, otherwise this process may fail\. After this process completes, the old KMS key may be safely retired\.