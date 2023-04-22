# Resilience in Amazon Connect<a name="disaster-recovery-resiliency"></a>

The AWS global infrastructure is built around AWS Regions and Availability Zones \(AZs\)\. AWS Regions provide multiple physically separated and isolated AZs, which are connected with low\-latency, high\-throughput, and highly redundant networking\. These AZs are physically separated by many miles, but still close enough together \(60 miles or less\) to be used as a single logical data center\. 

Each AZ features one or more discrete data centers, each housed in its own facility with redundant power, networking, and connectivity\. These measures act as safeguards, and minimize the likelihood of an issue like a power outage or earthquake impacting multiple data centers or multiple AZs\. 

AZs are more highly available, fault tolerant, and scalable than traditional single or multiple data center infrastructures\.

For more information about AWS Regions and Availability Zones, see [AWS Global Infrastructure](http://aws.amazon.com/about-aws/global-infrastructure/)\.

Amazon Connect runs on AWS proven infrastructure operating in multiple AZs within various geographic regions around the world\. This makes Amazon Connect more highly available, fault tolerant, and scalable than would be possible if a contact center solution was run from a single data center\. 

Within each AWS Region you can create an Amazon Connect instance, with a minimum of 3 AZs\. When you create an Amazon Connect instance, that instance is propagated across those AZs in an active\-active\-active configuration\. If there is a failure in one AZ, that node is taken out of rotation without impacting production\. This architecture allows you to perform maintenance, release new features, and expand infrastructure without requiring any downtime\.

## Single\-region telephony and softphone architecture<a name="telephony-recovery-resiliency"></a>

Amazon Connect is integrated with multiple telephony providers with redundant dedicated network paths to three or more AZs in every AWS Region where the service is offered today\. If a particular component, data center, or an entire AZ experiences failure, the affected endpoint is automatically taken out of rotation\. This allows you to continue providing a consistent quality experience for your customers\. 

Inbound \(US toll\-free\) and outbound calls in Amazon Connect are processed through multiple telecom carriers\. Each carrier is connected to multiple AZs in an active\-active configuration\. This ensures that impairment of a network path or an entire AZ does not impact your end\-customer experience\. It also ensures that inbound US toll\-free and outbound calls will be placed through multiple carriers so impairment at the carrier level doesn't impact your customer's experience\.

The following diagram illustrates this process: 

![\[Single-region telephony and softphone architecture.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/disaster-recovery-resiliency.png)

1. Callers reach your contact center using carriers that operate across multiple AZs at all times\.

1.  [RespOrg](https://en.wikipedia.org/wiki/RespOrg) routes US toll\-free traffic across multiple carriers in an active\-active fashion\.

1. Outbound calling is load balanced across multiple telephony providers\.

1. An agent's browser chooses from at least two servers across multiple AZs, based on reachability\.

## More resources<a name="more-resources-resiliency"></a>

To learn more about resiliency for Amazon Connect, the following resources from AWS Workshop Studio are highly recommended:
+ [Amazon Connect Global Resiliency Best Practices](https://catalog.workshops.aws/amazon-connect-global-resiliency/en-US/connectbestpractices) 
+ [Amazon Connect Global Resiliency and AWS Services Multi\-Region Best Practices](https://catalog.workshops.aws/amazon-connect-global-resiliency/en-US/awsservicesbestpractices) 