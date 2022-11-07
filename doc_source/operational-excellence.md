# Operational Excellence<a name="operational-excellence"></a>

Operational excellence includes the ability to run and monitor systems to deliver business value and continually improve supporting processes and procedures\. This section consists of design principles, best practices, and questions surrounding the operational excellence of Amazon Connect workloads\.

## Prepare<a name="prepare"></a>

Consider the following areas to prepare for an Amazon Connect workload\.

### AWS account<a name="awsaccount"></a>

With AWS Organizations, you can set up multiple AWS accounts for each level of your development, staging, and quality assurance environments\. This allows you to centrally govern your environment as you grow and scale your workloads on AWS\. Whether you are a growing startup or a large enterprise, Organizations helps you to centrally manage billing; control access, compliance, and security; and share resources across your AWS accounts\. This is the starting point for consuming AWS services along with a cloud adoption framework\. 

### Region selection<a name="regionselection"></a>

Amazon Connect Region selection is contingent upon data governance requirements, use case, services available in each Region, telephony costs in each region, and latency in relation to your agents, contacts, and external transfer endpoint geography\.

### Telephony<a name="telephony-bp"></a>
+ **Phone number porting** Open a porting request as far in advance of your pending go\-live date as possible\. 

  When porting phone numbers for critical workloads, include all requirements and use case information in your claim/port number several months before the go\-live date\. This includes requests for live cutover support, communication prior, during, and after cutover, monitoring, and anything else specific to your use case\. 

  For detailed information about porting your numbers, see [Port your current phone number](port-phone-number.md)\.
+ **Carrier diversity** In the US, you should use Amazon Connect telephony services for US toll\-free numbers, allowing you to route toll\-free traffic across multiple suppliers in an active\-active fashion at no additional charge\. In situations where you are forwarding inbound traffic to an Amazon Connect phone number, you should request redundant DID or Toll\-Free numbers across multiple telephony providers\. If you are claiming or porting multiple DID or Toll\-Free numbers outside of the US, you should request that those numbers be claimed or ported to a variety of telephony providers for increased resiliency\.
+ **International toll\-free and high\-concurrency DIDs** If you are using an existing toll\-free national service to redirect inbound traffic to DIDs, you should request DID phone numbers across multiple telephony providers\. A general recommendation for this configuration is 100 sessions per\-DID and your AWS Solutions Architect can help with capacity calculations and setup\.
+ **Testing** Thoroughly test all use case scenarios, preferably using the same or similar environment as your agents and customers\. Ensure that you test several inbound and outbound scenarios for quality of experience, Caller ID functionality, and measure latency to ensure it falls within acceptable range for your use case\. Any deviations from your target agent and customer environments need to be measured and accounted for\. For more information, including use case testing instructions and criteria, see [Troubleshooting Issues with the Contact Control Panel \(CCP\)](troubleshooting.md)\.

### Agent workstation<a name="agent-ws"></a>

The Amazon Connect Call Control Panel \(CCP\) has specific network and hardware requirements that must be met to ensure the highest quality of service for your agents and contacts:
+ Set Up Your Network for CCP use and ensure that your agent hardware meets minimum requirements\.
+ Ensure that you have used the Amazon Connect Check Amazon Connectivity Tool on the same network segment as your agents to verify that your network and environment is configured correctly for CCP use\.
+ Calculate PSTN latency for use cases that require agents and contacts to be in geographically distant locations
+ Review the [Troubleshooting Issues with the Contact Control Panel \(CCP\)](troubleshooting.md) section to create runbooks and playbooks for your agents and supervisors to follow should they encounter issues\. 
+ Set up monitoring for your agent workstations and consider partner solutions for call quality monitoring\. Your goal with monitoring your agent workstations should be the ability to identify the source of any potential network and resource contention\. For example, consider a typical agent’s softphone network connection path to Amazon Connect:  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/agentworkstation-oe.png)

  Without setting up monitoring at the local LAN/WAN, path to AWS, and agent workstation levels, it’s difficult and often impossible to determine if a voice quality issue is originating from your agent’s workstation, their private LAN/WAN, ISP, AWS, or the contact itself\. Setting up logging and alerting mechanisms proactively is critical in determining root cause and optimizing your environment for voice quality\.

### Configure your existing directory<a name="configure-directory"></a>

If you are already using an AWS Directory Service directory to manage users, you can use the same directory to manage user accounts in Amazon Connect\. This must be decided and configured when you create your Amazon Connect instance\. You cannot change the identity option you select after you create the instance\. For example, if you decide to change the directory you selected to enable Single Sign On \(SSO\) for your instance, you can delete the instance and create a new one\. When you delete an instance, you lose all configuration settings and metrics data for it

### Service Quotas<a name="service-quotas-bp"></a>

Review the default service quotas for each service involved in your workload as well as the default service quotas for Amazon Connect and request increases where applicable\. When requesting an increase for Amazon Connect, be sure to use expected values without additional padding for fluctuations\. Fluctuations are considered automatically when you make your request\.

### AWS Enterprise support<a name="enterprise-support-bp"></a>

AWS Enterprise Support is recommended for business and/or mission\-critical workloads on AWS\. Both Enterprise Support and Well\-Architected Review with an AWS Solutions Architect are required to qualify for the Amazon Connect Service Level Agreement\. 

### AWS well\-architected review<a name="well-architected-review-bp"></a>

Before any migration or implementation to Amazon Connect, follow our best practices by using the AWS Well\-Architected Framework, Operational Excellence\. The Framework provides a consistent approach for you to evaluate architectures and implement designs that will scale over time based on five pillars — operational excellence, security, reliability, performance efficiency, and cost optimization\. We also recommend using AWS Enterprise Support for business and mission\-critical workloads in AWS\. Both Enterprise Support and Well\-Architected Review with your AWS Solutions Architect are required to qualify for the Amazon Connect Service Level Agreement\. 

## Operate<a name="operate-bp"></a>

Consider the following areas to operate an Amazon Connect workload\.

### Logging and monitoring<a name="logging-monitoring-bp"></a>

See [Monitoring your instance using CloudWatch](monitoring-cloudwatch.md) and [Logging Amazon Connect API calls with AWS CloudTrail](logging-using-cloudtrail.md)\. 

### Contact attributes<a name="contactattributes-bp"></a>

Amazon Connect allows you to dynamically set and reference contact attributes within flows to create dynamic and personalized experiences for your contacts, create powerful self\-service applications, data\-driven IVRs, integrations with other AWS services, simplify phone number management, and allows for custom real\-time and historical reporting and analytics\. The following are Best practices and considerations you can follow to reduce complexity, prevent data loss, and ensure a consistent quality of experience for your contacts\.

Note the following considerations:
+ Data size – To prevent truncation, the size limitation for contact attributes you can set in a Set contact attributes block varies depending on the charset, encoding, and language used\. While this is generally enough data to play a short story for a contact, it is possible to exceed this limit, truncating any attributes set over the 32KB\. 
+ Data sensitivity – Note if any attributes being set, queried, and referenced are sensitive or fall under any regulatory guidelines and ensure that the data is being treated appropriately for your use case\. 
+ Data persistence – Any attributes set using the Set contact attributes block will be included in the contact record for your contact and available for screen pop to any custom agent desktop using the Streams API\. Any time the attribute is referenced within your flow and logging is enabled for the flow, the name and value of the attribute will be logged to Amazon CloudWatch\.

**Best practices**
+ Monitor usage – As you implement new functionality, onboard new business units, and iterate on existing flows, look up your current attribute usage in contact search, copy the attributes to a text editor, add the new attributes, and ensure that you do not exceed the 32KB size limitation\. Be sure to account for variable length fields like firstName and lastName and ensure that, even when the maximum space is used in a field, that you are still below the 32KB limitation\.
+ Clean\-up – If data persistence isn’t required, you can set an attribute with the same name and a blank value to prevent the data from being stored to the contact record or passed in a screen pop to an agent using the [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) API while freeing up the bytes that data would have otherwise used in the contact record\. 
+ Sensitive data – Use the **Store customer input** block to collect sensitive DTMF input from your contacts and use envelope encryption to protect both the raw data and the data keys used to encrypt them\. Store sensitive data in a separate database where persistence is required, use the **Set logging behavior** flow block to disable logging whenever sensitive information is referenced, and remove, clean up, or obfuscate sensitive data using the **Set contact attributes** block Clean\-up method outlined previously\. For more information, see [Compliance validation in Amazon Connect](compliance-validation.md)\. 

### Telephony<a name="telephony-bp"></a>

In the US, use toll\-free phone numbers wherever possible to load balance across multiple carriers for additional route and carrier redundancy\. This also helps to decrease time to resolution when compared to DID phone numbers, which must be managed by a single carrier\. In situations where you use DIDs, load balance across numbers from multiple carriers, when possible, to increase reliability\. Make sure that you handle all error paths in your flow appropriately, and implement the best practices, requirements, and recommendations located in [Troubleshooting Issues with the Contact Control Panel \(CCP\)](troubleshooting.md)\. 

If you’re forwarding your existing telephony provider’s phone numbers to Amazon Connect, ensure that the process to change the forward destination to an alternative DID/toll\-free number or otherwise remove the forward is defined and well\-understood by your operations team\. Ensure that you have Runbooks and Playbooks specifically for production readiness assessments, phone number porting and forwarding processes, and troubleshooting audio issues that could arise when transferring calls from your existing telephony provider\. You also want a repeatable process that your operations team can follow to determine if the source of these audio issues is Amazon Connect or your existing telephony provider\.

### Amazon Connect APIs<a name="apis-bp"></a>

Amazon Connect throttling quotas are by account, and not instance\. You should consider the following best practices when working with Amazon Connect APIs: 

#### Implement a caching/queuing solution<a name="queuingsolution"></a>

To decrease API data query overhead and avoid throttling, you can use an intermediary database like Amazon DynamoDB to store API call results rather than calling the API from all endpoints interested in the API data\. For example, the following diagram represents the use of the Amazon Connect metric API from multiple sources that need to consume this information:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/amazonconnectapis-oe.png)

Rather than having separate AWS Lambda functions, each with their own polling requirements, you can have a single AWS Lambda function write all interesting data to Amazon DynamoDB\. Rather than having each endpoint go to the API directly to retrieve the data, they point to DynamoDB, as illustrated in the following diagram:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/amazonconnectapis2-oe.png)

This architecture allows you to change polling intervals and add endpoints, as needed, without worrying about exceeding service quotas, giving you the ability to scale to however many concurrent connections your database solution supports\. You can use this same concept with querying any real\-time data feeds from Amazon Connect\. For situations where you need to perform an API action, like an Outbound API call, you can use this same concept in combination with Amazon Simple Queue Service to queue API requests Using AWS Lambda with SQS\.

#### Exponential back off and retry strategies<a name="retrystrategies"></a>

You can run into situations where API throttling limits get exceeded\. This can happen when the API calls fail and are retried repeatedly or made directly from multiple concurrent endpoints without a caching or queuing solution implemented\. To avoid exceeding your service quotas and impacting downstream processes, you should consider using exponential back off and retry strategies within your AWS Lambda functions in combination with caching and queueing\.

### Change management<a name="changemanagement"></a>

Two of the primary drivers for moving workloads to the Amazon Connect are flexibility and speed to market\. To ensure operational excellence without sacrificing agility, follow these best practices: 
+ **Modular flows**: Flows in Amazon Connect are similar to modern application building where smaller, purpose\-built components allow for more flexibility, control, and ease of management when compared to monolithic alternatives\. You can make your flows small and re\-usable, combining the modular flows into an end\-to\-end experience with **Transfer to flow** blocks\. This approach allows you to reduce risk during change implementation, allow you to test single, smaller changes rather than regression testing the entire experience, and will make it easier to identify and address issues with your flows during testing\. 
+ **Repositories**: Back up all versions of all ﬂows to a repository of your choice using contact ﬂow Import/Export as part of your change management process\. 
+ **Distribute by percentage**: To reduce risk encountered during change management and experiment with new experiences for your contacts, you can use the **Distribute by percentage** block to route a subset of your traffic to new flows while leaving the other traffic on the original experience\. 
+ **Measuring results**: Data driven decision making is key to successfully driving meaningful changes for your business\. Having a key metric to measure your changes against is absolutely necessary\. For all changes you’re making, you need to plan for how you will measure success\. For example, if you’re implementing self\-service functionality for your contacts, what percentage of contacts do you expect to self\-serve to consider the workload successful or what other metrics are you measuring to determine success? 
+ **Rollbacks**: Ensure that there is a clear, well\-defined, and well\-understood process to back out any changes to the previous state, specific to the change performed\. For example, if you publish a new flow version, ensure that the change instructions include documentation on how to roll back to the previous flow version\. 

### Routing profiles<a name="routingprofiles"></a>

Understanding how priority, delay, and overflow routing work within Amazon Connect is critical to maximizing agent productivity, reducing contact wait times, and ensuring the best quality of experience for your contacts\. 

### Routing in Amazon Connect<a name="routing-bp"></a>

Contact routing in Amazon Connect is done through a collection of queues and routing configurations called a routing profile\. A queue is equivalent to a skill or proficiency that agent needs to possess to service contacts for that queue\. A routing profile can be viewed a set of skills that you can match to your contact’s needs

Within your flow, you can prompt for additional information and, if they need to reach an agent, you can use the flow configuration to place them in the appropriate queue\. In the following example, Savings, Checking, and Loans are individual queues or skills and the three routing profiles are unique skillsets, or groups of skills:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/routingprofile1.png)

Each agent is assigned to only one routing profile based on their skillset, and many agents with similar skillset can share the same routing profile:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/routingprofile2.png)

Each phone number or chat endpoint will be associated with one flow\. The flow executes its logic, which may involve prompting the customer for information, to determine the contact’s needs, and eventually routes the contact into an appropriate queue\. The following diagram depicts how routing profile, queue, and flow work together to service a contact:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/routingprofile3.png)

To illustrate how you might determine various queues, routing profiles, and agent assignments to the routing profiles, consider the following table: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/routingprofile4.png)

On the top row, you’ve identified your skills or queues\. In the left column, you have your list of agents, and in the middle, you’ve checked the skills supported by each of the agents\. You can sort the matrix grouped by the common set of skill requirements across our agent population\. This helps identify the routing profiles as one marked in the green box \(which consists of two queues\), which you can assign agents to\. As a result of this exercise, you have identified four routing profiles, and assign your 13 agents to them accordingly\.

Based on the previous table, an incoming call from a contact needing the Savings skill could be served by three groups of agents in the three routing profiles 1, 2, and 4 as depicted in the following diagram:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/routingprofile5.png)

### Priority and delay<a name="prioritydelay-bp"></a>

Using the combination of priority and delay in different Routing Profiles, you can create flexible routing strategies\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/priorityandelay.png)

The preceding routing profile example shows a set of queues, and their respective priority and delay\. The lower the number, the higher the priority\. All higher priority calls must be processed before a lower priority call will be processed\. This is a difference from systems that will eventually process lower priority of calls based upon a weighting factor\.

You can also add a delay to each of the queues within each of the routing profiles\. Any call coming into the queue will be held for the specified period of delay assigned to the designated queue\. The call will be held for the delay period, even when agents are available\. You might use this in situations where you have a group of agents who are reserved to help you meet your Service Level Agreements \(SLAs\), but are otherwise assigned to other tasks or queues\. If a call doesn’t get answered within a specified period of time, these agents would become eligible to receive a call from the designated queue\. For example, consider the following diagram:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/priorityandelay2.png)

This diagram shows an SLA of 30 seconds\. A call comes in for the Savings queue\. The Savings queue immediately looks for an agent in the "Savings" routing profile due to the configuration of 0 delay in the profile for the queue\. Because of the configuration of 15 delay for Senior Agents, they will not be eligible to receive the Savings contact for 15 seconds\. After 15 seconds elapses, the contact becomes available for a Senior Level agent and Amazon Connect looks for the Longest Available across both routing profiles\.

### Path to service<a name="pathtoservice-bp"></a>

When you are designing customer experiences in Amazon Connect, plan to ensure a path to service\. There are many planned and unplanned events that can impact the customer experience as they traverse through Amazon Connect Flows\. The following sample customer experience shows some suggested checks to ensure a consistent quality experience for your contacts:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/pathtoservice.png)

This sample customer experience takes into account planned events such as Holidays and Business hours as well as unplanned events, like agents not staffed during business hours\. With this logic, you can also account for emergency situations, such as contact center closures because of inclement weather or service disruptions\. Consider the following concepts as illustrated in the diagram:
+ **Self\-service**: In a typical IVR, you can include any greetings and disclaimer messages such as call recording announcements upfront, which can be followed by self\-service options\. Self\-service brings cost and performance optimizations for your contact center and enables your organization to serve customers 24x7, regardless of holidays, business hours, or availability of agents\. Always include a path to service in case customers are unable to self\-serve and need human assistance\. For example, if you are using Amazon Lex bots for self\-service, you can make use of fallback intents to escalate conversations for human assistance\. 
+ **Holidays**: Many enterprise customers have a central repository that holds corporate holidays\. You can use an AWS Lambda function to data dip into that repository and offer holiday treatment to customers\. Additionally, you can also store corporate holidays in DynamoDB along with a custom message for each holiday\. For example, if your enterprise observes December 25 as Christmas, you could have a holiday prompt or Text to Speech, "We are currently closed for Christmas\. Please call back on December 26 when our normal business hours will resume\."  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/holidays.png)
+ **Business hours**: After holidays have been verified, you can check for business hours and, if outside of business hours, you can change the experience dynamically for your contacts\. If the contact occurs during business hours, you can identify customer intent for calls and map to certain queues in your contact center, increasing the likelihood of getting to the correct agent, and decreasing the amount of time it takes your contact to reach service\. It is highly recommended to map defaults as customers could be calling for a reason you haven’t accounted for yet or may respond in a way you don’t expect\.
+ **Emergency messages**: After you have identified customer intent for call, it is suggested to implement an emergency check treatment\. In the event of an emergency situation that impacts your contact center, you can store an emergency True/False flag in an intermediary database like DynamoDB\. To allow your supervisors and administrators to set this flag dynamically, with no code, you can build a separate IVR that authenticates your Amazon Connect administrators based upon ANI and PIN number verification for internal use only\. In the event of emergency, your supervisors can call into that dedicated line from their phones and after authentication set the Emergency flag to true for scenarios such as contact center closure due to inclement weather or ISP outage at the physical location of contact center\.
+ **Emergency message API**: You can also consider building an AWS API gateway with AWS Lambda function at the back end to set the Emergency flag to true/false securely in the database\. Your supervisors can securely access that API through web to toggle disaster mode or dynamically toggle it in response to an external event\. In your Amazon Connect instance, every contact that comes in through the flow will use AWS Lambda to check for that emergency flag and, in case of disaster mode, you can dynamically make announcements and provide a customer with a path to service\. This will further ensure business continuity and mitigate the impact of situations like these from affecting your customers\.
+ **Check agent staffing**: Before transferring to the queue in your flow, you can check agent staffing to ensure that an agent is logged in to service the contact\. For example, you may have an agent busy servicing another contact that might become available in the next five minutes, or you may not have anyone logged into the system at all\. During these instances, you will prefer a different customer experience rather than making them wait in the queue for an agent to become available\. 
+ **Route to service**: When you transfer the call to the queue, you can offer queued callbacks, queue overflows, or tiered routing using Amazon Connect routing profiles to offer a consistent, high\-quality experience for your callers that meet your Service Level requirements\.

## Resources<a name="operational-resources-bp"></a>

**Documentation**
+ [DevOps and AWS](http://aws.amazon.com/devops/)
+ [Amazon Connect Service API Documentation](https://docs.aws.amazon.com/connect/latest/APIReference/welcome.html)

**Blog**
+ [How to handle unexpected contact spikes with Amazon Connect](http://aws.amazon.com/blogs/contact-center/how-to-handle-unexpected-contact-spikes-with-amazon-connect/)

**Whitepaper**
+  [Operational Excellence Pillar](https://d0.awsstatic.com/whitepapers/architecture/AWS-Operational-Excellence-Pillar.pdf) 

**Video**
+ [DevOps at Amazon](https://www.youtube.com/watch?v=esEFaY0FDKc.pdf) 