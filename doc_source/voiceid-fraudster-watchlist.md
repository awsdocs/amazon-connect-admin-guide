# Create and edit a fraudster watchlist<a name="voiceid-fraudster-watchlist"></a>

Use the following APIs to create a fraudster watchlist and register fraudsters:

1. Use the [CreateWatchlist](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_CreateWatchlist.html) API to create new fraudster watchlists\. 

1. Use the [StartFraudsterRegistrationJob](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_StartFraudsterRegistrationJob.html) API for batch registration\. You can register new fraudsters to the new watchlist, or register them to the default watchlist that is associated with the Voice ID domain\.

When registering a new fraudster, Voice ID compares the voiceprint against all registers fraudsters in your Voice ID domain to determine if it is a duplicate of an existing fraudster\. 

To add fraudsters to a specified fraudster watchlist, pass the following data to the API:

1. The domain ID to specify the domain to associate recordings to\.

1. An input file containing a list of fraudsters\. See [Input and output file schema for Fraudster Registration Job](fraudster-registration-schema.md)\.

1. The location for output file\.

1. A KMS key to use when writing the output\.

1. A role that Voice ID can assume\. It must have access to the S3 bucket where the audio files are stored\. This role must have access to any KMS key used to encrypt the files\. It must also be able to write to the specified output location and use the KMS key requested for writing the output\. Specifically, it must have the following permissions:
   + `s3:GetObject` on the input bucket\.
   + `s3:PutObject` on the output bucket\.
   + `kms:Decrypt` on the KMS key used for input bucket’s default encryption\.
   + `kms:Decrypt` and `kms:GenerateDataKey` on the KMS key provided in the input which will be used for writing output file to the output bucket\.

   You must have `iam:PassRole` permissions when making the call and providing the `dataAccessRole`\. To enable confused deputy protection for the `dataAccessRole`, see [Amazon Connect Voice ID cross\-service confused deputy prevention](cross-service-confused-deputy-prevention.md#voiceid-cross-service)\.

1. A watchlistId to register the fraudster to\. If no watchlistId is specified, fraudsters are registered to the default watchlist for that Voice ID domain\.

1. The threshold for establishing the duplicate status of fraudsters\.

1. A flag to ignore fraudster duplicates\.

Voice ID updates the fraudster list with successful additions, and return a `GeneratedFraudsterID` associated with entry back to the same S3 location\. If duplicates are identified, Voice ID returns a "duplicate" status for the entry and provides the closest matching `GeneratedFraudsterId`\. After a fraudster is registered successfully, you can associate this fraudster identified by the `GeneratedFraudsterID` into a new watchlist by using the [AssociateFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_AssociateFraudster.html) API\. 

 Voice ID is not able to perform detection of fraudsters in a watchlist before the fraudster list is created\. 

For quotas for the fraudster list, see [Amazon Connect service quotas](amazon-connect-service-limits.md)\.

**Note**  
You are charged for adding to the fraudster list\. For more information, see [Amazon Connect Voice ID Pricing](http://aws.amazon.com/connect/voice-id/)\.