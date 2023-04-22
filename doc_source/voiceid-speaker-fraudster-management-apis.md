# Voice ID speaker, watchlist, and fraudster management APIs<a name="voiceid-speaker-fraudster-management-apis"></a>

Amazon Connect Voice ID includes APIs to manage speakers enrolled into a Voice ID domain and fraudsters registered in the domain\. All speaker APIs, except `ListSpeakers`, accept either the `CustomerSpeakerId` or `GeneratedSpeakerId`\. 

## Speaker management APIs<a name="speaker-management-apis"></a>

1.  [DescribeSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeSpeaker.html): Describe a speaker's [status in a domain \(ENROLLED, OPTED\_OUT, EXPIRED\)](voiceid-domain.md#voiceid-speaker-enrollments), and to map a `GeneratedSpeakerId` to a `CustomerSpeakerId`, and vice versa\. 

1.  [DeleteSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteSpeaker.html): Completely remove all records for a caller/speaker from a Voice ID domain\. All voiceprints and enrollment status is deleted immediately, and associated audio recordings are removed within 24 hours\. 

1.  [ListSpeakers](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListSpeakers.html): List all the speakers whose entries are present in a Voice ID domain\. This API returns both the `CustomerSpeakerId` and `GeneratedSpeakerId` for a speaker\. It returns a paginated output with the page size dictated in the API request\.

1. [OptOutSpeaker](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_OptOutSpeaker.html): Opt out a caller from a Voice ID domain\. This API doesn't require the speaker to be present in Voice ID\. A non\-existing speaker can be opted\-out using this API and Voice ID persists the opted out status and rejects future enrollment requests for this speaker\. Opting out also removes voiceprints and any stored audio recordings for this caller\.

## Watchlist management APIs<a name="watchlist-management-apis"></a>

1.  [CreateWatchlist](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_CreateWatchlist.html): Create a watchlist that fraudsters can be a part of\.

1.  [DeleteWatchlist](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteWatchlist.html): Remove a custom fraudster watchlist from the Voice ID domain\. To delete a watchlist, it must be empty\. That is, it must not have any fraudsters associated to it\. You can use the [DeleteFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteFraudster.html) or [DisassociateFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DisassociateFraudster.html) APIs to remove all fraudsters from a watchlist\. 

   You cannot delete the default watchlist from a Voice ID domain\.

1.  [DescribeWatchlist](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeWatchlist.html): Determine if it is a default fraudster watchlist, or a custom watchlist that you created, and obtain watchlist details\.

1.  [ListWatchlists](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListWatchlists.html): List all the watchlists in the Voice ID domain\.

1. [UpdateWatchlist](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_UpdateWatchlist.html): Update the name and description of a custom fraudster watchlist\. You cannot modify details of the default watchlist because it's managed by Voice ID\.

## Fraudster management APIs<a name="fraudster-management-apis"></a>

1.  [AssociateFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_AssociateFraudster.html): Associate a fraudster to a watchlist in the same domain\. You can associate a fraudster to multiple watchlists in a domain\.

1. [DeleteFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DeleteFraudster.html): Delete a fraudster from a Voice ID domain\. Deleting the fraudster removes the fraudster from all watchlists it is a part of\. It also deletes all voiceprints and associated audio recordings within 24 hours\.

1.  [DescribeFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DescribeFraudster.html): Describe a fraudster's status in the Voice ID domain\.

1.  [DisassociateFraudster](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_DisassociateFraudster.html): Disassociate a fraudsters from the watchlist specified\. Note that a fraudster always has to be associated with at least one fraudster watchlist; an exception is thrown if you try to disassociate a fraudster from its only watchlist\. 

   To remove the fraudster completely, use `DeleteFraudster`\. 

1.  [ListFraudsters](https://docs.aws.amazon.com/voiceid/latest/APIReference/API_ListFraudsters.html): List all the fraudsters in a domain or a specific watchlist\. This API also returns the watchlists the fraudster is a part of\. It returns a paginated output with the page size dictated in the API request\.