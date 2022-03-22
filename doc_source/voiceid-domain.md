# Voice ID domains<a name="voiceid-domain"></a>

When you enable Amazon Connect Voice ID, you create a Voice ID domain: a container for all Voice ID data, such as speaker identifiers \(which serves as the customer identifier\), the voiceprints, the customer audio that was used for creating the enrollment voiceprints, and the enrollment statuses \(enrolled, opted out, etc\.\) associated with the speaker identifiers\. For detection of fraudsters in a watchlist, the Voice ID domain stores the fraudster identifiers, voiceprints, and audio used for creating the voiceprints\.

Following are guidelines for creating Voice ID domains: 
+ Each Amazon Connect instance can be associated with only one Voice ID domain\. 
+ Each Voice ID domain can be associated with multiple Amazon Connect instances\. This enables you to use the same stored customer data across multiple Amazon Connect instances\.
+ You can create multiple domains, but they don't share customer data between each other\. 
+ We recommend creating a new Voice ID domain to associate with a Amazon Connect instance when: 
  + You are enabling Voice ID for the first time on your account in an AWS Region\.
  + You want to ensure that you isolate the Voice ID domains used for your test and production environments\.
+ We recommend using an existing Voice ID domain when: 
  + You want to use the same set of enrolled callers and fraudsters across different Amazon Connect instances \(that may belong to different customer service teams\) 
  + You want to use the same test environment across different test Amazon Connect instances\.
**Note**  
Only existing Voice ID domains in the same Region in your Amazon Connect account can be shared across Amazon Connect instances in that Region\.
+ You can change the association of your Amazon Connect instance from your current domain to a new domain at any time, by choosing a different domain\. 
+ To delete a Voice ID domain, use the [DeleteDomain](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteDomain.html) Voice ID API\. `DeleteDomain` soft deletes the domain\. Amazon Connect waits 30 days before completely erasing the domain data\. During this period, Voice ID; is disabled for all the Amazon Connect instances it is associated with\. To restore a domain during this window, submit an AWS Support ticket and provide the domain ID\. You can find the domain ID on the Voice ID section of the Amazon Connect console, as shown in the following example:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-domain.png)

  Deleting a Voice ID domain deletes all stored customer data, such as audio recordings, voiceprints, and speaker identifiers, as well as any fraudster watchlists that you managed\.

## Enrollment status<a name="voiceid-speaker-enrollments"></a>

Voice ID stores three different enrollment status for a speaker: `ENROLLED`, ` OPTED_OUT` and `EXPIRED`\. You can recall these speaker status using [Amazon Connect Voice ID APIs](https://docs.aws.amazon.com/voiceid/latest/APIReference/) and using contact flow blocks to take appropriate action\.
+ `ENROLLED`: When you enroll a new caller is enrolled into Voice ID, Voice ID creates a new voiceprint and set the speaker status as `ENROLLED`\. Even if you re\-enroll the same caller into Voice ID, the status stays as `ENROLLED`\.
+ `OPTED_OUT`: If a caller does not provide consent to enroll into biometrics, you can opt out the caller \(in the Contact Control Panel\) or using APIs\. Voice ID creates a new entry for this caller and set the speaker's status `OPTED_OUT`\. Voice ID does not generate any voiceprint or store any audio recording for the speaker\. Future enrollment requests for this speaker is rejected unless their entry is deleted\.
+ `EXPIRED`: If a caller's voiceprint has not been accessed or refreshed for 3 years, Voice ID changes the status to `EXPIRED`, and you are no longer able to perform authentications for this caller\. You can re\-enroll the caller again or delete the caller from Voice ID\.

## Speaker and fraudster identifiers<a name="voiceid-speaker-identifiers"></a>

Voice ID uses speaker identifiers to refer to and retrieve the voiceprints in a Voice ID domain\. We recommend that you use identifiers that do not contain an Personally Identifiable Information \(PII\) in the identifiers\. 

Voice ID creates two fields to refer to a caller: 
+ `CustomerSpeakerId`: A identifier provided by the customer\. It can be between 1\-256 characters and can only contain: **a\-z**, **A\-Z**, **0\-9**, **\-** and **\_**
+ `GeneratedSpeakerId`: A unique 22\-character alphanumeric string that Voice ID creates and returns at the time of enrollment of the caller\.

[Amazon Connect Voice ID speaker APIs](https://docs.aws.amazon.com/voiceid/latest/APIReference/Welcome.html) accept either form of speaker identifiers, but only emit `GeneratedSpeakerId` in the Voice ID event streams and contact records\. If you want to re\-record the caller to redo the voiceprint, you can enroll the caller with the same `CustomerSpeakerId`\. 

 Similarly, Voice ID creates unique fraudster identifiers called `GeneratedFraudsterID` for every fraudster that you add to a watchlist in the domain\. Voice ID returns the fraudster identifier if a fraudster is detected in a call when performing fraud risk detection\. 