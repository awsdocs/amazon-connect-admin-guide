# Input and output file schema for Speaker Enrollment Job<a name="speaker-enrollment-job-schema"></a>

## Input file schema<a name="speaker-enrollment-input-schema"></a>

Following is the schema of the input manifest file for the Speaker Enrollment Job:

```
{
  "Version": "string",
  "SpeakerEnrollmentRequests": [
      {
          "RequestId": "string",
          "SpeakerId": "string",
          "AudioSpecifications": [
              {
                  "S3Uri": "string",
                  "ChannelId": number 
              }
           ] 
      }
   ]
}
```

**Note**  
All the fields in the schema are **required**\.

Following is a description of each attribute of the input schema\.
+ `Version`: The version of the input schema document\. Currently, this should be `1.0`\.
+ `SpeakerEnrollmentRequests`: List of speaker enrollment requests to be fulfilled as part of the job\.
  + `RequestId`: An identifier for this speaker enrollment request\. It must be unique within the input file\. It is used for mapping and identifying entries in the output file\.
  + `SpeakerId`: The client\-provided identifier of the speaker who needs to be enrolled\. You must pass the `CustomerSpeakerId` in this field\. The `GeneratedSpeakerId` is not currently supported\.
  + `AudioSpecifications`: The list of audio files that Voice ID can use for enrolling this speaker\. Voice ID uses these audio files together to gather required amount of speech for enrollment\. Currently, the maximum number of audio files allowed for an enrollment request is **10**\. Each file can be a \.wav file up to 20MB, containing audio with 8KHz sample rate and PCM\-16 encoding\.
    + `S3URI`: The Amazon S3 location of the audio file in \.wav format that needs to be used for enrolling the speaker\. 
    + `ChannelId`: The audio channel to be used for enrolling the speaker in a multi\-channel audio file\. Voice ID supports audio files with up to two channels, so this value is restricted to either **0** or **1**\.

## Output file schema<a name="speaker-enrollment-output-schema"></a>

Following is the schema of the output file generated for the Speaker Enrollment Job:

```
{
  "Version": "string",
  "Errors": [
       {
          "RequestId": "string",
          "ErrorCode": number,
          "ErrorMessage": "string"
       }
   ],
   "SuccessfulEnrollments": [
       {
          "RequestId": "string",
          "GeneratedSpeakerId": "string",
          "CustomerSpeakerId": "string",
          "EnrollmentStatus": "DUPLICATE_SKIPPED" | "NEW_ENROLLMENT" | "ENROLLMENT_OVERWRITE"
       }
   ]   
}
```

Following is a description of each attribute of the output schema\.
+ `Version`: The version of the output schema document\. Currently, this should be `1.0`\.
+ `Errors`: The list of errors for the speaker enrollment requests that failed at some point during enrollment\.
+ 
  + `RequestId`: The request identifier associated with this request\. This is the same as the `RequestId` specified in the input file for this request\.
  + `ErrorCode`: The HTTP error code representing the type of error\. Some example error scenarios are described below\. 
**Note**  
This is not an exhaustive list\.
    + 400 \(Bad Request Exception\): 
      + The input JSON file is malformed and cannot be parsed\.
      + The provided audio files do not have enough speech for enrollment\.
      + Fraud verification checks failed for the given speaker\.
    + 402 \(ServiceQuotaLimitExceededException\):
      + Speaker limit exceeded\.
    + 409 \(Conflict Exception\):
      + Conflicting action: You cannot request an enrollment for an opted out speaker\.
    + 500 \(Internal Failure\):
      + Internal Server Error \(Unexpected error on the Service\-side\)\.
  + `ErrorMessage`: A message describing the cause of the enrollment failure\.
+ `SuccessfulEnrollments`: The list of enrollment requests that succeeded\.
  + `RequestId`: The request identifier associated with this request\. This is the same as the `RequestId` specified in the input file for this request\.
  + `CustomerSpeakerId`: The client\-provided identifier for the speaker who was enrolled\.
  + `GeneratedSpeakerId`: The service\-generated identifier for the speaker who was enrolled\.
  + `EnrollmentStatus`: The status of successful speaker enrollment
    + `DUPLICATE_SKIPPED`: The speaker is already enrolled, and the enrollment was skipped\.
    + `NEW_ENROLLMENT`: The speaker was newly enrolled into the system\.
    + `ENROLLMENT_OVERWRITE`: The speaker is already enrolled, but was re\-enrolled/overwritten using the new audio\.