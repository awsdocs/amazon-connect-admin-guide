# Performance efficiency<a name="performance-efficiency-bp"></a>

Performance eﬃciency includes the ability to use computing resources eﬃciently to meet system requirements, and to maintain that eﬃciency as demand changes and technologies evolve\. This section provides an overview of design principles, best practices, and questions surrounding performance efficiency for Amazon Connect workloads\. You can ﬁnd prescriptive guidance on implementation in the [Performance Eﬃciency Pillar](                 https://d0.awsstatic.com/whitepapers/architecture/AWS-Performance-Efficiency-Pillar.pdf) whitepaper\.

## Architectural design<a name="performance-efficiency-architecturaldesignbp"></a>

There are two fundamental architectural design principles to consider when designing experiences for the contact center: 
+ Reductionism is a philosophical tenet stating that by analyzing a system to its ultimate component parts, you can unravel it at deeper levels\. 
+ Holism, in contrast, states that by considering the whole picture one gets a deeper and more complete view of a situation than by analyzing it into its component parts 

The reductionist approach focuses on each individual component \(IVR, ACD, Speech Recognition\) on its own and often results in a disjointed customer experience that, when evaluated individually, may meet performance requirements for the use case\. However, when evaluated end\-to\-end, can result in decreased quality of experience for your contacts while funneling development efforts into operational silos\. This approach complicates regression testing, increases time to market, and limits the development of cross\-discipline operational resources critical to the success of your contact center\.

A holistic view of the contact center is shown in the following diagram:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/architecturaldesign.png)

The holistic approach results focus on a more complete and cohesive experience for customers, and not which technology will provide which part of that experience\. 

Let the customer and what they want define and guide your efforts\. The experiences that you create for your contacts should not be static or an end state, but should serve as a starting point that should be iterated on continuously based on customer feedback\. The regular collection and review of operational and tuning data surrounding how your contacts are interacting and navigating throughout their journey should drive that iteration\. Your goal should be dynamic and personalized experiences for contacts reaching your company\. This can be accomplished through dynamic data\-driven contact design and routing, resulting in an experience that conforms to your contact and their individual needs\.

You can start with the default experience, building out your contact flows, but refactoring your single contact flow into two to enable future segmentation:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/architecturaldesign2.png)

In your next iteration, identify additional experiences that you need to plan for and build routing and, if necessary, contact flows for each\. For example, you may want to play different prompts for a contact that is past due on their bill or that may have tried to contact multiple times for the same purpose\. With this approach, you are working towards personalized, dynamic experiences that are pertinent to your contacts and why they are contacting you\. In addition to improving the quality of experience for your contacts and decreasing handle times, you’re encouraging contact self\-service by providing a more intelligent and flexible experience\. Your next iteration may look like the following illustration:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/architecturaldesign3.png)

## Contact flow design<a name="contactflowdesign-bp"></a>

A contact flow defines the customer experience with your contact center from start to finish\. Your contact flow configuration can have a direct impact on performance, operational efficiency, and ease of maintenance\. 

Many Large businesses support multiple phone numbers, business units, prompts, queues, and other Amazon Connect resources\. While it is possible to have unique contact flows for each phone number and line of business, it can lead to a one\-to\-one mapping of phone numbers and contact flows\. This results in unnecessary service quota requests and a large number of contact flows to support and maintain\. A one\-to\-one mapping of DNIS and Contact flow implementation is illustrated in the following figure:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/contactflowdesign.png)

Alternatively, you should consider an approach that results in Multiple DNIS to one or few contact flows by using the dynamic nature of Amazon Connect contact flows\. With this approach, you can store configuration information like Prompts, Queues, Business Hours, Whisper Prompts/Flows, Queues, Queue Treatments and Hold Messages etc\., in NoSQL Database DynamoDB\. In Amazon Connect, you can associate multiple phone numbers to the same contact flow and use the Lambda function to look up configurations for that phone number\. This allows you to dynamically define the contact’s experience based on the attributes returned from DynamoDB\. 

For example, you can play prompts or use Text\-to\-Speech \(TTS\) to greet callers based upon the lookups in DynamoDB or associate queues using dynamic attributes supported in contact flow blocks\. The result with this approach is a contact flow implementation that is efficient to build, maintain, and support: 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/contactflowdesign2.png)

## Load testing<a name="loadtesting-bp"></a>

If you need to run load or scale testing, you can employ third\-party or partner solutions to run load tests, or develop your own custom solution using the Amazon Connect [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API to generate calls combined with browser automation scripts to simulate agent behavior\. Before to performing load tests, review and follow the [Amazon Connect Load Testing Policy](http://aws.amazon.com/connect/testing/)\. 

## Agent enablement<a name="agentenablement-bp"></a>

Amazon Connect provides a readily available browser\-based Contact Control Panel \(CCP\) for agents to interact with customer contacts\. Your agents use the CCP to accept contacts, chat with contacts, transfer them to other agents, put them on hold, and perform other key tasks\. You can realize significant performance efficiency through the creation of custom agent desktop solutions using the [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) API\. Consider using the Streams API to increase performance efficiency in the following areas:
+ CRM integration \- The Streams API allows you to embed the CCP in your CRM application, create your own interface, or integrate with other AWS services and partner solutions to provide your agents with the tools and resources they need to service your contacts\. With a custom desktop, like the Amazon Connect and [Salesforce integration](salesforce-integration.md), your agents can get a comprehensive view of customer and contact in a single interface without managing multiple screens and interfaces\. 
+ Authentication \- You can configure SAML for identity management in Amazon Connect and use AWS SSO \(SSO\) to allow your agents to use the same credentials they use to access your other systems and avoid the need to enter them multiple times\. 
+ Agent automation \- In addition to streamlining your agent experience, you can automate common, repeatable tasks\. For example, automatically creating cases or pre\-filling webforms and offering a screen pop with relevant information when a contact is offered\. This can reduce handle times and improve the quality of experience for your agents and contacts\. 
+ Enhanced capabilities \- You can also enhance/extend the CCP functionality to include real\-time [Transcriptions, Translations, Suggested Actions and Knowledge base integrations](http://aws.amazon.com/solutions/implementations/ai-powered-speech-analytics-for-amazon-connect/)\. Integrating enhanced capabilities with your agent desktop will allow skilled agents to service contacts more efficiently and unskilled agents to provide service when skilled agents aren’t available\. For example, you can use this approach to automatically translate a chat contact for unskilled agent that doesn’t know the language\. When your agent replies, you can automatically translate the text to the contact’s language, allowing for real\-time bilingual communication\. 

## Using other AWS services<a name="leveragingotherservices-bp"></a>

This section discusses AWS services that you can use to improve performance, identify areas of opportunity, and gain valuable insights into your contact data\. 

### AWS Lambda<a name="lambda-bp"></a>

You can use AWS Lambda in your Amazon Connect contact flows to perform data dips for customer information, send SMS text messages, and with other services like Amazon S3 to automatically distribute scheduled reports\. For more information, see [Best Practices for Working with AWS Lambda functions](https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html)\. 

### AWS Direct Connect<a name="directconnect-bp"></a>

AWS Direct Connect is a cloud service solution that makes it more efficient to establish a dedicated network connection from your premises to AWS\. It provides a durable, consistent connection rather than relying on your ISP to dynamically route requests to AWS resources\. It allows you to configure your edge router to redirect AWS traffic across dedicated fiber rather than traversing the public WAN and establish private connectivity between AWS and your data center, office, or colocation environment\. In many cases, this can reduce your network costs, increase bandwidth throughput, and provide a more consistent network experience than Internet\-based connections\. 

While AWS Direct Connect does not solve issues specific to private LAN/WAN traversal to your edge router, it can help solve for latency and connectivity issues between your edge router and AWS resources\. It can also solve for latency and poor call quality between your edge router and AWS resources\. 

Depending on your VDI environment, you may not be able to take advantage of AWS Direct Connect as it requires you to conﬁgure your edge router to redirect AWS traﬃc across dedicated ﬁber rather than traversing the public WAN\. If the VDI environment is hosted outside of your local DXC\-enabled network, you may not be able to take full advantage of AWS Direct Connect\.

Do not use AWS Direct Connect for “QoS” or “increased security\.” AWS Direct Connect can cause performance degradation in cases where the latency from the agent workstation is higher than the ISP’s path to the Amazon Connect instance\. AWS Direct Connect does not offer additional security when compared to an ISP as Amazon Connect voice and data is already encrypted\.

### Amazon Polly<a name="amazonpolly-bp"></a>

Amazon Connect offers a native integration with Amazon Polly, allowing you to play dynamic and natural Text\-to\-Speech \(TTS\), use Speech Synthesis Markup Language \(SSML\), and take advantage of Neural Text\-to\-Speech \(NTTS\) to achieve the most natural and human\-like text\-to\-speech voices possible\. 

### Amazon Lex<a name="amazonlex-bp"></a>

Your contact’s path to service can be a challenging experience that doesn’t always meet up to their expectations\. Your contacts may wait on hold, repeat information, need to be transferred, and ultimately, spend too much time getting what they need\. AI is playing a role in improving this customer experience in call centers to include engagement through chatbots — intelligent, natural language virtual assistants\. These chatbots are able to recognize human speech and understand the caller’s intent without requiring the caller to speak in specific phrases\. Contacts can perform tasks such as changing a password, requesting a balance on an account, or scheduling an appointment without ever speaking to an agent\.

Amazon Lex is a service that allows you to create intelligent conversational chatbots\. It lets you turn your Amazon Connect contact center contact flows into natural conversations that provide personalized experiences for your callers\. Using the same technology that powers Amazon Alexa, an Amazon Lex chatbot can be attached to your Amazon Connect contact flow to recognize the intent of your caller, ask follow\-up questions, and provide answers\. Amazon Lex maintains context and manages the dialogue, dynamically adjusting the responses based on the conversation, so your contact center can perform common tasks for callers, to address many customer inquiries through self\-service interactions\. Additionally, Amazon Lex chatbots support an optimal \(8 kHz\) telephony audio sampling rate, to provide increased speech recognition accuracy and fidelity for your contact center voice interactions\.

Building an effective Amazon Lex bot requires providing simple and realistic utterances as training sets to the bot, periodically reviewing your bot’s performance, updating your utterance set, and modifying the bot based on such a review\. For more information, see the following resources: 
+ [Monitoring in Amazon Lex](https://docs.aws.amazon.com/lex/latest/dg/monitoring-aws-lex.html)
+ [Building Better bots using Amazon Lex](http://aws.amazon.com/blogs/machine-learning/building-better-bots/)

### Amazon Kinesis<a name="amazonkinesis-bp"></a>

For situations where you need to gain additional insight from your contact metrics and real\-time data from Amazon Connect, you can:
+ Export your contact record data to Amazon Redshift using Amazon Kinesis\.
+ Use Amazon Kinesis video stream \(KVS\) and AWS Lambda to transcribe call recordings or voice contacts in real\-time using Amazon Transcribe and send the resulting text to Amazon Comprehend for sentiment analysis\.
+ Leverage the [Amazon Connect Agent Event Kinesis Stream](agent-event-streams.md) for real\-time agent CTI and schedule adherence data\.

### Amazon OpenSearch Service and Kibana<a name="kibana-bp"></a>

Using Amazon OpenSearch Service and Kibana to process real\-time Amazon Connect data gives you a flexible way to query and visualize real\-time and historical Amazon Connect data beyond native reporting capabilities\.

### Amazon Connect Contact Lens<a name="contactlens-bp"></a>

Contact Lens for Amazon Connect is a set of machine learning \(ML\) capabilities integrated into Amazon Connect that allow contact center supervisors to better understand the sentiment, trends, and compliance risks of customer conversations to effectively train agents, replicate successful interactions, and identify crucial company and product feedback\. Contact Lens for Amazon Connect transcribes contact center calls to create a fully searchable archive and surface valuable customer insights\.

## Resources<a name="performance-resources-bp"></a>

**Documentation**
+ [Best practices design patterns: optimizing Amazon S3 performance](https://docs.aws.amazon.com/AmazonS3/latest/userguide/optimizing-performance.html) 
+ [ Amazon EBS volume performance on Linux instances](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSPerformance.html)

**Whitepaper**
+ [Performance Eﬃciency Pillar](                         https://d0.awsstatic.com/whitepapers/architecture/AWS-Performance-Efficiency-Pillar.pdf)

**Video**
+ [AWS re:Invent 2016: Scaling Up to Your First 10 Million Users \(ARC201\)](https://www.youtube.com/watch?v=n28lDDdlnVg) 
+ [AWS re:Invent 2017: Deep Dive on Amazon EC2 Instances](https://www.youtube.com/watch?v=mZy6E2I5Rek) 