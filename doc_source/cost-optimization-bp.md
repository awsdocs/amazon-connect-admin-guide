# Cost optimization<a name="cost-optimization-bp"></a>

Cost Optimization includes the ability to run systems to deliver business value at the lowest price point\. This section provides an overview of design principles, best practices, and questions surrounding cost optimization for Amazon Connect workloads\. You can ﬁnd prescriptive guidance on implementation in the Cost Optimization Pillar whitepaper\. 

There are five areas to consider for cost optimization for Amazon Connect workloads\.

## Region selection<a name="regionselection-co"></a>

Amazon Connect Region selection is one of the first decision customers make when adopting Amazon Connect for their contact center workloads\. While latency and voice quality are important aspects to Region selection, you should evaluate Region selection from a cost perspective as well\. Telephony pricing for Claimed Phone Numbers Per Day and Per Minute Inbound Usage can be different for countries depending upon the AWS Region in which you select to instantiate your Amazon Connect Instance\. You can find telephony price for each Region at [Amazon Connect Pricing](http://aws.amazon.com/connect/pricing/) page\. 

## Callbacks<a name="callbacks-co"></a>

You can provide a callback in your flow for callers during high call volume periods or long wait times\. You can use callbacks to reduce cost and improve the quality of experience for your contacts\. When your contact opts\-in for the callback, Amazon Connect will retain the position in the queue and allow the caller to disconnect\. When an agent becomes available to service your contact, Amazon Connect will place an outbound call to the number configured to connect the contact to your agent\. A sample callback flow is included in every instance at creation\. You can also use AWS Lambda and Amazon DynamoDB to prevent duplicate callback requests\.

## Storage<a name="storage-co"></a>

With Amazon Connect, you can configure your instance and flows to store call recordings and chat transcripts of caller’s interactions for compliance, quality monitoring, and training purposes\. Voice contacts are not recorded unless an agent is connected to the caller\. If multiple agents are connected, each will have an associated call recording or transcript\. Amazon Connect stores voice recordings in Amazon S3 according to your Amazon S3 Lifecycle policy configuration\. With the call recordings stored in Amazon S3, you can use Amazon S3 tiers of storage to manage retention and optimize cost\. For example, you can transition objects using Amazon S3 Lifecycle to move call recordings and transcripts over three months old to S3 Glacier to reduce storage cost\.

## Self\-service<a name="selfservice-co"></a>

Amazon Connect’s pay\-as\-you\-go pricing model can result in lower costs as compared to traditional licensing\-based contact centers\. However, the traditional contact center infrastructure that spans automatic call distribution \(ACD\) systems, IVR, telephony and work force management \(WFM\) systems plays a proportionately small contribution to the overall cost of contact center operations\. The largest contributor to the cost of the contact center often comes from human capital and the real estate required to provide an operating environment for your agents\. Amazon Connect Flows can be used natively with Amazon Lex for NLU, NLP, and ASR and Amazon Polly for lifelike Text\-to\-Speech \(TTS\) to build highly engaging user experiences and natural conversational interactions across voice and text\. By using an Amazon Lex chatbot in your Amazon Connect call center, callers can perform tasks such as changing a password, requesting a balance on an account, or scheduling an appointment, without needing to speak to an agent\. These self\-service options result in better customer experience and lowers your cost per contact\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/selfservice.png)

## Click\-to\-call<a name="clicktocall-co"></a>

You can use click\-to\-call in Amazon Connect to initiate a voice call using the [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html) API for authentication through web or mobile application to reduce call handle times and improve the quality of experience\. With this approach, you’re able to offer your contact the ability to bypass IVR authentication, pass contextual information like URLs, recent web/mobile activity, and user data to your flows to create dynamic, personalized experiences\. For example, a contact browsing your website to purchase an item or member of a financial institution who is already authenticated in the mobile app and wants to speak with an agent about a recent transaction\.

## Redirect voice contacts to chat<a name="redirectvoiccecontactstochat-co"></a>

With Amazon Connect, you can allow agents to handle multiple chat conversations simultaneously where they would only able to handle one voice conversation\. When you don't have a voice agent available, you can send an SMS text message to your customer to offer a link to chat with an agent right away\.

## Resources<a name="costoptimization-resources-bp"></a>

**Documentation**
+  [Analyzing Your Costs with Cost Explorer](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/ce-what-is.html) 
+  [AWS Cloud Economics Center](http://aws.amazon.com/economics/) 
+ [What are AWS Cost and Usage Reports](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html) 

**Whitepaper**
+ [Cost Optimization Pillar](https://d0.awsstatic.com/whitepapers/architecture/AWS-Cost-Optimization-Pillar.pdf) 