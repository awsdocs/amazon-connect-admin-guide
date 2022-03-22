# Voice ID speaker and fraudster management APIs<a name="voiceid-speaker-fraudster-management-apis"></a>

Amazon Connect Voice ID includes APIs to manage speakers enrolled into a Voice ID domain and fraudsters registered in the domain\. All speaker APIs except `ListSpeakers` accept either the `CustomerSpeakerId` or `GeneratedSpeakerId`\. 

1.  [DescribeSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeSpeaker.html): Use this API to describe a speaker's [status in a domain \(ENROLLED, OPTED\_OUT, EXPIRED\)](voiceid-domain.md#voiceid-speaker-enrollments), and to map a `GeneratedSpeakerId` to a `CustomerSpeakerId`, and vice versa\. 

1. [OptOutSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_OptOutSpeaker.html): To opt out a caller from a Voice ID domain, you can use this API\. This API doesn't require the speaker to be present in Voice ID\. A non\-existing speaker can be opted\-out using this API and Voice ID persists the opted out status and rejects future enrollment requests for this speaker\. Opting out also removes voiceprints and any stored audio recordings for this caller\.

1.  [DeleteSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteSpeaker.html): To completely remove all records for a caller/speaker from a Voice ID domain, you can use this API\. All voiceprints and enrollment status is deleted immediately, and associated audio recordings are removed within 24 hours\. 

1.  [ListSpeakers](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListSpeakers.html): To list all the speakers whose entries are present in a Voice ID domain, you can use this API, which returns both the `CustomerSpeakerId` and `GeneratedSpeakerId` for a speaker\. It returns a paginated output with the page size dictated in the API request\.

1.  [DescribeFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeFraudster.html): You can use this API to describe a fraudster's status in the Voice ID domain\.

1. [DeleteFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteFraudster.html): To delete a fraudster from a Voice ID domain, you can use this API\. It deletes all voiceprints and any stored audio recordings\. 