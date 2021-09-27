# Batch enrollment using audio data from prior calls<a name="voiceid-batch-enrollment"></a>

You can get a jump start on using biometrics by batch enrolling customers who have already consented for biometrics\. Using stored audio recordings in your S3 bucket, and a JSON input file that provides the speaker identifier and a link to the audio recordings, you can invoke the [Voice ID batch](https://docs.aws.amazon.com/voiceid/APIReference/API_StartSpeakerEnrollmentJob.html) APIs\. 

To enroll customers programmatically, pass the following data to the API:

1. The domain ID to specify the domain to associate recordings to\.

1. The location for the output file\.

1. An input file containing a list of speakers\. See [Input and output file schema for Speaker Enrollment Job](speaker-enrollment-job-schema.md)\. 

    For each speaker the file must include:
   + A link to a call audio recording\.
   + The corresponding `CustomerSpeakerId` for the customer\.
   + A channel for the caller in the audio recording\. If the audio has multiple channels, you can select only one\.

1. A KMS key to use when writing the output\.

1. A role that Voice ID can assume\. It must have access to the S3 bucket where the audio files are stored\. This role must have access to any KMS key used to encrypt the files\. It must also be able to write to the specified output location and use the KMS key requested for writing the output\. Specifically, it must have the following permissions:
   + `s3:GetObject` on the input bucket\.
   + `s3:PutObject` on the output bucket\.
   + `kms:Decrypt` on the KMS key used for input bucket’s default encryption\.
   + `kms:Decrypt` and `kms:GenerateDataKey` on the KMS key provided in the input which will be used for writing output file to the output bucket\.

   You must have `iam:PassRole` permissions when making the call and providing the `dataAccessRole`\. 

1. Optionally, a fraud check skip flag in case you want to skip fraud checking on the enrollment audio\.

1. Optionally, the fraud threshold in case you want to raise or lower the risk\.

1. Optionally, a flag to re\-enroll enrolled customers\. This is useful if you want to refresh the audio recording, since the default is to ignore previously enrolled customers\.

The batch enrollment returns the `CustomerSpeakerId`, `GeneratedSpeakerId`, and associated status for each entry\. It stores this data in a JSON file at the output path you specify in the API\.

**Note**  
You are charged for enrolling speakers\. For more information, see [Amazon Connect Voice ID Pricing](http://aws.amazon.com/connect/pricing/voice-id/)\.