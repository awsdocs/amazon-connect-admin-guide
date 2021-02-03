# Resilience in Amazon Connect<a name="disaster-recovery-resiliency"></a>

The AWS global infrastructure is built around AWS Regions and Availability Zones\. AWS Regions provide multiple physically separated and isolated Availability Zones, which are connected with low\-latency, high\-throughput, and highly redundant networking\. With Availability Zones, you can design and operate applications and databases that automatically fail over between Availability Zones without interruption\. Availability Zones are more highly available, fault tolerant, and scalable than traditional single or multiple data center infrastructures\. 

For more information about AWS Regions and Availability Zones, see [AWS Global Infrastructure](http://aws.amazon.com/about-aws/global-infrastructure/)\.

In addition to the AWS global infrastructure, Amazon Connect offers the following features to help support your data resiliency and backup needs:
+ [Contact flow versioning](rollback.md) 
+ Ability to export your CTR data to Kinesis\. This way, you can back up the CTR data across Availability Zones\. 

To backup call recordings, use the [cross\-region replication](https://docs.aws.amazon.com/AmazonS3/latest/dev/replication.html) \(CRR\) feature to copy the call recordings to Amazon S3 buckets in different AWS Regions\.