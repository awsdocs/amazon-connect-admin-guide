# Scenario and deployment approaches<a name="scenario-deployment-approaches"></a>

Amazon Connect offers self\-service configuration and enables dynamic, personal, and natural customer engagement at any scale with a variety of migration and integration options\. In this section, we explain the following scenarios and deployment approaches to consider when designing a workload for Amazon Connect:
+ Traditional contact center
+ Inbound
+ Outbound
+ Hybrid contact center
+ Legacy contact center migration
+ Virtual desktop infrastructure \(VDI\)

## Traditional contact center<a name="traditional-contact-center"></a>

The traditional contact center requires a significant telephony, media, networking, database, and compute infrastructure footprint that can span multiple vendors and data center locations to service contacts\. Each individual solution and vendor have unique hardware, software, networking, and architectural requirements that have to be met while resolving versioning, compatibility, and licensing conflicts\. 

It is common to have separate vendors and infrastructure requirements for local and remote agent hardware and VPN connectivity, Text\-To\-Speech \(TTS\), Automatic Call Distribution \(ACD\), Interactive Voice Response \(IVR\), voice audio and data, physical desk phones, voice recording, voice transcriptions, chat, reporting, database, Computer Telephony Integration \(CTI\), Automatic Speech Recognition \(ASR\), and Natural Language Understanding \(NLP\)\. Your contact center architecture and infrastructure becomes more complicated when you consider multi\-stage development, quality assurance, and test environments\. 

![\[Traditional contact center.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/traditionalcontactcenter.png)

A typical Amazon Connect deployment solves or reduces many of the challenges associated with versioning, compatibility, licensing, contact center telephony infrastructure, and maintenance\. It gives you the flexibility to create instances in new locations in minutes and migrate components individually, or in parallel, to best meet your individual business objectives\. You can use flows for your IVR/ACD, have voice and data delivered through a supported web browser to your agent’s softphone, port your existing phone numbers, redirect softphone audio to an existing desk phone, invoke an Amazon Lex bot natively within your flow for ASR and NLP, and use the same flow for chat and voice\. You can use Amazon Contact Lens to automatically generate voice transcriptions, perform key word identification and sentiment analysis, and categorize contacts\. For agent CTI data and real\-time voice streaming, you can use Amazon Connect Agent Event Streams and Kinesis Video Streams\. You can also create multi\-stage development, quality assurance, and test environments at no additional cost and only pay for what you use\.

## Inbound<a name="inbound"></a>

Inbound is a contact center term used to describe a communication request initiated by a contact to the center\. Contacts can reach your Amazon Connect instance for inbound self\-service or to speak with a live agent in a variety of ways, including voice and chat\. Voice contacts go through the PSTN and are routed to the Amazon Connect Instance telephony entry point through the phone number claimed in your instance\. You can reserve a phone number with Amazon Connect directly, port your existing phone number, or forward voice contacts to Amazon Connect\. Amazon Connect can provide local and toll\-free numbers in all Regions where the service is supported\.

![\[Inbound contacts.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/inbound.png)

When a phone call is placed to a number claimed in or ported to your Amazon Connect instance, the flow associated with the called number will be invoked\. You can define the flow using flow blocks that can be configured with no coding knowledge required\. The flow determines how the contact should be processed and routed, optionally prompting the contact for additional information to assist in routing decisions, storing those attributes to the contact details, and, if necessary, routing that contact to an agent with all of the call details and transcripts gathered along the way\. Through the flow, you can invoke AWS Lambda functions to query customer information, call other AWS services like Amazon Pinpoint to send SMS text messages, and use native AWS service integrations including Amazon Lex for NLU/NLP and Kinesis Video Streams for real\-time streaming of voice calls\. 

If an inbound contact needs to reach an agent, the contact is put into a queue and routed to an agent when they change their status to Available, according to your routing configuration\. When the available agent’s contact is accepted manually or through auto\-accept configuration, Amazon Connect connects the contact with the agent\. 

![\[Contact in a queue.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/inbound2.png)

 When an inbound contact comes from a browser or mobile app request for a chat session, the request is routed to a web service or Amazon API Gateway endpoint that calls the Amazon Connect chat API to invoke the flow configured in your request\. You can use the same flows for chat and voice, where the experience is managed and routed dynamically, based on the logic defined in the flow\.

## Outbound<a name="outbound"></a>

Amazon Connect allows you the ability to programmatically make outbound contact attempts to local and international endpoints, reduce agent set\-up time between contacts, and improve agent productivity\. By using the [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) API and [StartOutboundVoiceContact](https://docs.aws.amazon.com/connect/latest/APIReference/API_StartOutboundVoiceContact.html), you can develop your own outbound solution or take advantage of existing partner integrations that work with your CRM data to create dynamic, personalized experiences for your contacts and empowering your agents with the tools and resources they need to service those contacts\. 

Outbound campaigns are typically driven by contact data exported from CRMs and separated into contact lists\. Those contacts are prioritized and either delivered to the agents to initiate after a period of preview or programmatically contacted using the Amazon Connect Outbound API, driven by your flow logic, and connecting to agents as needed\. Typical outbound contact center use cases include fraud and service alerts, collections, and appointment confirmations\.

## Hybrid<a name="hybrid"></a>

If you have requirements to transfer contacts between Amazon Connect and legacy contact center technologies, you can use a Hybrid model architecture to pass contact data with the transfer\. For example, a sales business unit on a legacy contact center platform may need to transfer a call to the service business unit that’s been migrated to Amazon Connect\. Without a Hybrid architecture, call details will be lost and may require the contact to repeat information\. This could increase handle times and may result in contact calling again for the same purpose\. 

Hybrid architectures require you to claim as many phone numbers as your expected maximum concurrent contacts and an intermediary state database accessible by both Amazon Connect and your legacy contact center platform\. When a transfer is required to the other platform, you will use one of these phone numbers as a unique identifier, flag it as in\-use in your intermediary database, insert your contact details, and use that number as your ANI or DNIS when you transfer the contact\. When the contact is received by the other contact center platform, you will query the intermediary database for the contact details based on the unique ANI or DNIS you used\. Hybrid architectures are typically used as an interim migration step because of the additional cost and complexity associated\.

### IVR\-only<a name="ivr-only"></a>

You may choose to use Amazon Connect to drive the contact’s IVR experience while your agent population remains on your legacy contact center platform\. With this approach, you can use Amazon Connect flows to drive self\-service and routing logic, and, if necessary, transfer the contact to the target agent or agent queue on your legacy contact center platform\. 

![\[IVR only.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/hybridivr.png)

In this diagram, the contact dials a phone number claimed in your Amazon Connect instance for service\. If they need to be transferred to an agent on your legacy contact center platform, an AWS Lambda function is invoked to query an available unique phone number, flag it as in\-use, and write relevant contact details to an intermediary database\. The contact is then transferred to the legacy contact center platform with the phone number returned from the Lambda function\. The legacy contact center will then perform a query on the intermediary database for the contact details, route accordingly, and reset the contact data in the intermediary database, allowing the phone number to be used again\.

### Agent\-only<a name="agent-only"></a>

With this approach, your legacy contact center IVR drives the contact’s IVR self\-serve and routing logic, and, if necessary, transfers the contact to Amazon Connect to route to your agent population\.

![\[Agent only.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/hybridagentonly.png)

In this diagram, the contact dials a phone number claimed with your legacy contact center platform\. If they need to be transferred to an agent on Amazon Connect, the legacy contact center platform will query an available unique phone number, flag it as in\-use, and write relevant contact details to an intermediary database\. The contact will then be transferred to Amazon Connectwith the phone number returned by the legacy contact center’s query\. Amazon Connect will then query the contact details from the intermediary database using AWS Lambda, route accordingly, and reset the contact data in the intermediary database, allowing the phone number to be used again\.

### Mixed<a name="mixed"></a>

In this scenario, you may have your IVR and agents operating in parallel on Amazon Connect and your legacy contact center platform to allow for site, agent group, or line\-of\-business migrations\.

![\[Mixed.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/hybridmixed.png)

## Legacy contact center migration<a name="legacy-contact-center-migration"></a>

When you are evaluating Amazon Connect for new or existing workloads, there are several strategies you can consider\. For situations that require contact details to be included when contacts are transferred between Amazon Connect and your legacy contact center solution, a Hybrid model architecture will be required until the migration is complete\. The approaches described in this section allow you to move specific lines of business in phases, manage training and support, and mitigate risks associated with change\.

### New workload<a name="new-workload"></a>

You may decrease risk associated with changes to existing business units and increase flexibility and digital innovation potential by adopting a net new workload on Amazon Connect\. Net new workloads that do not require the Hybrid model architecture are less complex, are not affected by change in business process or agent routine, and have a faster time to market\. Adopting a net new workload allows you to take advantage of usage\-based, pay\-as\-you\-go pricing\. Your contact center resources are available to create a new experience for their end users, test and implement it to evaluate the platform, gain confidence, and build the skills and operational mechanisms to prepare for larger migration across existing workloads\.

### IVR First<a name="ivr-first"></a>

You may choose to use Amazon Connect to drive the contact’s IVR experience while your agent population remains on your legacy contact center platform\. With this approach, you can use Amazon Connect Flows to drive self\-service and routing logic, and, if necessary, transfer the contact to the target agent or agent queue on your legacy contact center platform\. 

### IVR Last<a name="ivr-last"></a>

With this approach, your legacy contact center IVR drives the contact’s IVR self\-serve and routing logic, and, if necessary, transfers the contact to Amazon Connect to route to your agent population\.

### Line of business segmentation<a name="lob-segmentation"></a>

If your lines of business have separate IVRs or don’t require contact transfers to legacy contact center platforms, you may want to consider a line of business migration approach\. For example, selecting your service desk for internal support as your first line of business to migrate\. After migrating your service desk IVR and agent population to Amazon Connect, you may choose to forward your existing contact to Amazon Connect, porting the endpoint after testing and business validation is completed\. 

### Site or agent group segmentation<a name="agent-segmentation"></a>

If your contact center has a global footprint, services contacts from multiple countries, or is managed independently by a respective geography or location, you may want to consider a migration approach based on a physical site or geography of agents\. Each agent population and/or geography can have its own unique requirements and considerations that may not apply globally\. Approaching your migration this way will allow each site or agent group to gain the skills they need to continue to operate independently before moving onto the next\.

## Virtual desktop infrastructure \(VDI\)<a name="vdi"></a>

While you can use the Amazon Connect Contact Control Panel \(CCP\) within Virtual Desktop Infrastructure \(VDI\) environments, it will add another layer of complexity to your solution that warrants separate POC efforts and performance testing to optimize\. The configuration/support/optimization is best handled by your VDI support team and the following deployment models are the most commonly implemented\.

### VDI client with local browser access<a name="vdi"></a>

You can build a custom CCP with the [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) API by creating a CCP with no media for call signaling\. This way, the media is handled on the local desktop using standard CCP, and the signaling and call controls are handled on the remote connection with the CCP with no media\. The following diagram describes that approach:

![\[VDI client with local browser access.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/vdi.png)

### VDI client without local browser access<a name="vdi"></a>

Sometimes the VDI client does not have access to a local browser\. In this scenario, you can create a single CCP instance with media run from the VDI server allowing access to enterprise resources\. For this deployment model UDP audio is usually enabled on the VDI OS\. This deployment model requires extensive testing to calibrate the different VDI server parameters to optimize quality of experience:

![\[VDI client without local browser access.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/architecture/vdinobrowser.png)