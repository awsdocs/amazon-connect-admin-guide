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
+ **Voiceprints** – When Amazon Connect Voice ID is enabled, a voiceprint is created from the customer's voice for future authentication\. Similarly, a voiceprint is created while registering a fraudster in the Voice ID system for future fraud detection\.
+ **Speaker and Fraudster Audio** – When Amazon Connect Voice ID is enabled, the audio used for enrolling speakers and registering fraudsters is stored so that Voice ID can re\-enroll and reregister them in future when there is a need to do so\.

Amazon Connect stores the following Personally Identifiable Information \(PII\) data related to your customers:
+ The customer's phone number: ANI for inbound calls, and DNIS for outbound calls or transfers\.
+ If you are using Amazon Connect Customer Profiles, all this data could potentially be PII\. This data is always encrypted at rest using either a customer\-provided KMS key or a service\-owned key\. The Amazon Connect Customer Profiles data is segregated by the AWS account ID and the domain\. Multiple Amazon Connect instances can share a single Customer Profiles domain\.
+ For Amazon Connect High\-Volume Outbound Communications, Amazon Pinpoint passes customer phone numbers and relevant attributes to Amazon Connect\. On the Amazon Connect side, these are always encrypted at rest using either a customer managed key or an AWS owned key\. The Amazon Connect High\-Volume Outbound Communications data is segregated by the Amazon Connect instance ID and are encrypted by instance\-specific keys\.

## External application data<a name="external-application-data"></a>

Amazon AppIntegrations enables you to integrate with external applications\. It stores references to other AWS resources and client\-service specified metadata\. No data is stored other than incidentally while being processed\. When syncing data periodically with an Amazon Connect service, data is encrypted using a customer managed key and stored temporarily for one month\. 

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

Contact data classified as PII that is stored by Amazon Connect is encrypted at rest using a key that is time\-limited and specific to the Amazon Connect instance\. Specifically, the customer origination phone number is cryptographically hashed with a key that is specific to the instance to allow for use in contact search\. For contact search, the encryption key is not time\-sensitive\. 

The following data stored by Amazon Connect is treated as sensitive:
+ Origination phone number
+ Outbound phone number
+ External numbers dialed by agents for transfers
+ External numbers transferred to by a contact flow
+ All contact attributes

## Contact Lens real\-time processing<a name="real-time-processing-data"></a>

Content processed by Contact Lens in real\-time is encrypted at rest and in transit\. Data is encrypted with keys owned by Contact Lens\.

## Voiceprints and Voice ID audio recordings<a name="voiceprints-data-protection"></a>

When you enable Amazon Connect Voice ID, it computes voiceprints out of your customer's speech for authenticating them in future, and stores the data\. Similarly, when you enable fraud detection, it stores the voiceprint for each fraudster registered in Voice ID\. 

While enrolling a customer into Voice ID for authentication and fraud detection, you must specify a `CustomerSpeakerId` for them\. Since Voice ID stores biometric information for each speaker, we strongly recommend that you use an identifier that does not contain PII in the `CustomerSpeakerId` field\. 

## Speaker and Fraudster Audio<a name="speaker-fraudster-audio-data-protection"></a>

When you enable Amazon Connect Voice ID, it stores the necessary amount of audio it aggregated while enrolling a speaker or registering a fraudster into the system\. The data is retained until the speaker/fraudster is deleted\. This audio is used in the future whenever the voiceprints for the speakers and fraudsters need to be regenerated\.

## High\-Volume Outbound Communications<a name="outbound-communications-data-protection"></a>

For Amazon Connect High\-Volume Outbound Communications, Amazon Pinpoint passes customer phone numbers and relevant attributes to Amazon Connect\. On Amazon Connect, these are always encrypted at rest using either a customer managed key or an AWS owned key\. The Amazon Connect High\-Volume Outbound Communications data is segregated by the Amazon Connect instance ID and are encrypted by instance specific keys\.