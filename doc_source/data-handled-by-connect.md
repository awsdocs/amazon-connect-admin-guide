# Data handled by Amazon Connect<a name="data-handled-by-connect"></a>

Data held within Amazon Connect is segregated by the AWS account ID and the Amazon Connect instance ID\. This ensures that data can be accessed only by the authorized users of a specific Amazon Connect instance\.

Amazon Connect handles a variety of data related to the contact center, including but not limited to the following categories\. 
+ **Resources and configurations** \-\- This includes queues, contact flows, users, and routing profiles\.
+ **Contact metadata**\-\- This includes connection time, handle time, source number \(ANI\), destination number \(DNIS\), and user defined contact attributes\.
+ **Agent\-related performance data** \-\- This includes login time, status changes, and contacts handled\.
+ **Phone call audio streams** \-\- When enabled, this also includes call recordings\.
+ **Chat transcripts** – Included only if enabled\.
+ **Attachments** – Included only if enabled\.
+ **Integration configuration** – Includes user defined name, description and metadata when creating integration with external applications\.
+ **Knowledge documents** – This includes documents used by agents to handle contacts\.
+ **Voiceprints** – When Amazon Connect Voice ID is enabled, a voiceprint is created from the customer's voice for future authentication\.

Amazon Connect stores the following Personally Identifiable Information \(PII\) data related to your customers:
+ The customer's phone number: ANI for inbound calls, and DNIS for outbound calls or transfers\.
+ If you are using Amazon Connect Customer Profiles, all this data could potentially be PII\. This data is always encrypted at rest using either a customer\-provided KMS key or a service\-owned key\. The Amazon Connect Customer Profiles data is segregated by the AWS account ID and the domain\. Multiple Amazon Connect instances can share a single Customer Profiles domain\.

Amazon AppIntegrations, which enables you to integrate with external applications, stores references to other AWS resources such as Amazon EventBridge buses and rules, and client\-service specified metadata\. No third party data is stored other than incidentally while being processed\.

## Phone call media<a name="phone-call-media-handling"></a>

Amazon Connect is in the audio path for calls handled by the service\. It is therefore responsible for relaying the call’s media stream between participants\. This can include the audio between a customer and a contact flow / IVR, the audio between a customer and an agent, or mixing the audio between multiple parties in a conference or during a transfer\. There are two types of phone calls:
+ PSTN calls\. This includes inbound customer calls, outbound calls placed by agents to customers, and calls to an agent’s physical phone, if this option has been enabled in the Contact Control Panel \(CCP\)\.
+ Softphone calls placed to the agent’s browser\.

PSTN calls are connected between Amazon Connect and various telecommunications carriers using either private circuits maintained between Amazon Connect and our providers or existing AWS internet connectivity\. For PSTN calls routed over the public internet, signaling is encrypted with TLS and the audio media is encrypted with SRTP\.

Softphone calls are established to the agent’s browser with an encrypted WebSocket connection using TLS\. The audio media traffic to the browser is encrypted in transit using DTLS\-SRTP\.

## Call recordings<a name="call-recording-handling"></a>

Call recording is disabled by default in Amazon Connect\. You can enable call recording in the contact flows, which allows for more detailed control over which calls are recorded\. 

The call recording feature has options for choosing whether to record the agent only, customer only, or agent and customer conversations\. When call recording is enabled, the recording begins when the call is connected to an agent and stops when the agent disconnects\. Any transfers to external numbers are not recorded after the agent leaves the call\.

You can limit access to the call recordings based on user permissions\. Recordings can be searched and played back within the Amazon Connect web interface\.

### Call recording storage<a name="call-recording-storage"></a>

Call recordings are stored in two phases:
+ Recordings intermediately held within Amazon Connect during and after the call, but before delivery\.
+ Recordings delivered to your Amazon S3 bucket\.

The recordings that are stored in your Amazon S3 bucket are secured using a AWS KMS key that was configured when your instance was created\. 

At all times, you maintain full control over the security of call recordings delivered to your Amazon S3 bucket\.

### Call recording access<a name="call-recording-access"></a>

You can search and listen to call recordings in Amazon Connect\. To determine which users can do this, assign them the appropriate security profiles\. If AWS CloudTrail is enabled, access to specific recordings by Amazon Connect users is captured in CloudTrail\. 

The capabilities of Amazon S3, AWS KMS, and IAM put you in full control of who has access to call recording data\.

In addition, you can track who listens to or deletes recordings; see [Track who deleted or listened to recordings](track-who-deleted-recordings.md)\. 

## Contact metadata<a name="contact-metadata"></a>

Amazon Connect stores metadata related to contacts that flow through the system and allows authorized users to access this information\. The Contact Search feature allows you to search and view contact data, such as origination phone numbers or other attributes set by the contact flow, that are associated with a contact for diagnostics or reporting purposes\. 

Contact data classified as PII, or data that represents customer content being stored by Amazon Connect, is encrypted at rest using a key that is time\-limited and specific to the Amazon Connect instance\. Specifically, the customer origination phone number is cryptographically hashed with a key that is specific to the instance to allow for use in contact search\.

The following data stored by Amazon Connect is treated as sensitive:
+ Origination phone number
+ Outbound phone number
+ External numbers dialed by agents for transfers
+ External numbers transferred to by a contact flow
+ All contact attributes

## Contact Lens real\-time processing<a name="real-time-processing-data"></a>

Content processed by Contact Lens in real\-time is encrypted at rest and in transit\. Data is encrypted with keys owned by Contact Lens\.

## Voiceprints<a name="voiceprints-data-protection"></a>

If you enable Amazon Connect Voice ID, it computes and stores voiceprints out of your customers’ speech for authenticating them in future\. You must specify a Speaker ID for each customer while enrolling them for Voice ID\. We strongly recommend that you use an identifier that does not contain PII for this field\.

In the preview release of Voice ID, the audio data used for generating enrollment and authentication voiceprints is enqueued for deletion within 24 hours\.