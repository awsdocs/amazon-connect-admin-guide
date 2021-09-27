# Input and output file schema for Fraudster Registration Job<a name="fraudster-registration-schema"></a>

## Input file schema<a name="fraudster-registration-input-schema"></a>

Following is the schema of the input manifest file for Fraudster Registration Jobs:

```
{
 "Version": "string",
    "FraudsterRegistrationRequests": [
       {
           "RequestId": "string",
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
+ `Version`: The version of the schema document\. Currently, this should be `1.0`\.
+ `FraudsterRegistrationRequests`: List of fraudster registration requests to be fulfilled as part of the job\.
  + `RequestId`: An identifier for this fraudster registration request\. It must be unique within the input file\. It is used for mapping and identifying entries in the output file\.
  + `AudioSpecifications`: The list of audio files that Voice ID can use for registering this fraudster\. Voice ID uses these audio files together to gather required amount of speech for registration\. Currently, the maximum number of audio files allowed for a registration request is **10**\.
    + `S3URI`: The Amazon S3 location of the audio file in \.wav format that needs to be used for registering the fraudster\. 
    + `ChannelId`: The audio channel to be used for registering the fraudster in a multi\-channel audio file\. Voice ID supports audio files with up to two channels, so this value is restricted to either **0** or **1**\.

## Output file schema<a name="fraudster-registration-output-schema"></a>

Following is the schema of the output manifest file for Fraudster Registration Jobs:

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
   "SuccessfulRegistrations": [
       {
          "RequestId": "string", 
          "GeneratedFraudsterId": "string", 
          "RegistrationStatus": "DUPLICATE_SKIPPED" | "NEW_REGISTRATION",
          "FraudsterSimilarityScore": number
       }
   ]   
}
```

Following is a description of each attribute of the output schema\.
+ `Version`: The version of the output schema document\. Currently, this should be `1.0`\.
+ `Errors`: The list of errors for the fraudster registration requests that failed at some point during registration\.
+ 
  + `RequestId`: The request identifier associated with this request\. This is the same as the `RequestId` specified in the input file for this request\.
  + `ErrorCode`: The HTTP error code representing the type of error\. Some example error scenarios are described below\. 
**Note**  
This is not an exhaustive list\.
    + 400 \(Bad Request Exception\): 
      + The input JSON file is malformed and cannot be parsed\.
      + The provided audio files do not have enough speech for registration\.
    + 402 \(ServiceQuotaLimitExceededException\):
      + Fraudster limit exceeded\.
    + 500 \(Internal Failure\):
      + Internal Server Error \(Unexpected error on the Service\-side\)\.
  + `ErrorMessage`: A message describing the cause of the fraudster registration failure\.
+ `SuccessfulRegistrations`: The list of registration requests that succeeded\.
  + `RequestId`: The request identifier associated with this request\. This is the same as the `RequestId` specified in the input file for this request\.
  + `RegistrationStatus`: The status of successful fraudster registration\.
    + `DUPLICATE_SKIPPED`: The fraudster was identified as a duplicate, and the registration was skipped\.
    + `NEW_FRAUDSTER`: The Fraudster was newly enrolled into the system\.
  + `GeneratedFraudsterId`: The service\-generated identifier for the fraudster who was registered\. In case the `RegistrationStatus` is `DUPLICATE_SKIPPED`, this is the identifier of the fraudster already in the domain that is the closest match to the given fraudster\.
  + `FraudsterSimilarityScore`: An optional field that is populated when the fraudster registration is skipped due to it being a duplicate\. This represents the similarity of the given fraudster with the closest matching fraudster already existing in the domain\.