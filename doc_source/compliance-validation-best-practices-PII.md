# Best practices for PII compliance in Amazon Connect<a name="compliance-validation-best-practices-PII"></a>

Following this list of best practices can help you ensure your Amazon Connect contact center is PII \(Personally Identifiable Information\) compliant\. 
+ Conduct compliance eligibility audits for all services used in your contact center, as well as any third party integration points\.
+ AWS Key Management Service \(KMS\) encrypts Amazon S3 contents at the object level, which covers recordings, logs, and saved reports by default for Amazon S3\. Make sure encryption in transit and at rest rules apply downstream or to third party apps\. 
+ Use encryption in the **Store customer input** block for sensitive DTMF information\.
+ Use your own KMS key when ingesting data in Amazon Connect Customer Profile domains\.
+ As with any AWS service, we strongly recommend that you not use sensitive information to name resources\.