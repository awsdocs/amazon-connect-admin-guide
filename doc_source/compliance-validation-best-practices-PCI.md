# Best practices for PCI compliance in Amazon Connect<a name="compliance-validation-best-practices-PCI"></a>

Following this list of best practices can help you ensure your Amazon Connect contact center is PCI\-compliant\. 
+ Conduct compliance eligibility audits for all services used in your contact center, as well as any third party integration points\.
+ Payment card information \(PCI\) should be collected via encrypted DTMF\.
+ If PCI is captured in call recordings, the PCI data must be scrubbed from the recording and obfuscated from any logs or transcriptions\. We recommend working with an Amazon Solution Architect if you need help doing this\. 
+ Use encryption in transit and at rest for any downstream integration points\.
+ Enable multi\-factor authentication \(MFA\) for any access to PCI as Amazon Connect is a public endpoint\.
+ For a detailed walkthrough that explains how to encrypt PCI, see [Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)\. 
+ AWS Key Management Service \(KMS\) encrypts Amazon S3 contents at the object level, which covers recordings, logs, and saved reports by default for Amazon S3\. Make sure encryption in transit and at rest rules apply downstream or to third party apps\. 
+ Use encryption in the **Store customer input** block for sensitive DTMF information\.
+ For more information, see [ https://www\.pcisecuritystandards\.org]( https://www.pcisecuritystandards.org)\. 