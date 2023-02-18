# Search and review Voice ID results<a name="voiceid-ctr-fields"></a>

Use the [Contact search](contact-search.md) page to search for and review the results of enrollment status, voice authentication, and detection of fraudsters in a watchlist\. With the required [ security profile permissions](contact-search.md#required-permissions-search-contacts) \(**Analytics and Optimization** \- **Voice ID \- attributes and search \- View**\), you can search for Voice ID results using the following filters:
+ **Speaker actions**: Use this filter to search for contacts where the caller was enrolled into Voice ID or chose to opt\-out of Voice ID altogether\.
+ **Authentication result**: Use this filter to search for contacts where Voice ID authentication returned the following results: 
  + Authenticated
  + Not authenticated
  + Opted out
  + Inconclusive
  + Not enrolled

  For example, if you want to search for all contacts where the authentication status was returned as **Not authenticated** or **Opted out**, select both these options and choose **Apply**\.
+ **Fraud detection result**: Use this filter to search for contacts where Voice ID fraud analysis returned the following results: 
  + High risk for fraud
  + Low risk for fraud
  + Inconclusive
+ **Fraud detection reason**: Use this filter to search for contacts where specific fraud risk mechanisms were detected:
  + Known fraudster: the caller’s voice matches a fraudster from the fraudster watchlist you have created\.
  + Voice spoofing: the caller is modifying their voice or is using speech synthesis to spoof the agent\.

## Voice ID results in a Contact Record<a name="voiceid-ctr"></a>

After you search for a contact, you can choose an ID to view their contact record\. The following image shows an example of the fields in the Voice ID section of the contact record: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/voiceid-ctr-nospoofing.png)