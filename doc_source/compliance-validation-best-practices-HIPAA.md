# Best practices for HIPAA compliance in Amazon Connect<a name="compliance-validation-best-practices-HIPAA"></a>

**Note**  
Amazon Connect Wisdom is currently not HIPAA compliant\.

**Note**  
Amazon Connect Voice ID is not currently HIPPA compliant\.

Following this list of best practices can help you ensure your Amazon Connect contact center is HIPAA compliant\. 
+ Conduct compliance eligibility audits for all services used in your contact center, as well as any third party integration points\.
+ AWS Key Management Service \(KMS\) encrypts Amazon S3 contents at the object level, which covers recordings, logs, and saved reports by default for Amazon S3\. Make sure encryption in transit and at rest rules apply downstream or to third party apps\. 
+ Use encryption in the **Store customer input** block for sensitive DTMF information\.
+ Do not upload content subject to HIPPA to Amazon Connect Wisdom\.
+ For more information about HIPAA compliance, see [https://www\.hipaacompliance\.org/](https://www.hipaacompliance.org/)\.