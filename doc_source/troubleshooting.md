# Amazon Connect Troubleshooting and Best Practices<a name="troubleshooting"></a>

Use this guide to identify best practices for using Amazon Connect\. Also, to troubleshoot information when something isn't working quite how it should\.

**Topics**
+ [Best Practice for Using the Contact Control Panel](#bp-ccp)
+ [Troubleshooting Issues with the CCP](#trb-ccp)
+ [Validation Testing](#valid-testing)

## Best Practice for Using the Contact Control Panel<a name="bp-ccp"></a>

This guide provides information about the CCP soft phone, including best practices and troubleshooting\. For workstations unable to meet soft phone connectivity requirements or experiencing soft phone issues, the CCP also features the ability to redirect to an external device\.

**Topics**
+ [Agent Workstation Requirements](#ccp-agent-hardware)
+ [Network Ports and Protocols](#ccp-networking)
+ [Using Amazon Connect in a VDI Environment](#using-ccp-vdi)
+ [CCP Connectivity](#ccp-connectivity)

### Agent Workstation Requirements<a name="ccp-agent-hardware"></a>

Agent workstations in the contact center vary widely\. While the Amazon Connect CCP is built to handle high levels of jitter and high latency environments, the architecture of the workstations that agents use, and the location and environment in which they take calls, can impact the quality of experience\.

Under\-powered workstations can make it difficult for agents to access the tools and resources they need to service callers\. Also, keep in mind the resource requirements when scoping workstations to ensure that they can perform under load while appropriately multitasking for the use case\. For the best agent and customer audio experience, a USB headset is recommended\. Alternatively, you can redirect the call to an external number, in E\.164 format, using an agent's existing telephony\.

 The following values are the minimum system requirements for the workstations using the CCP only\. Additional memory, bandwidth, and CPU should be scoped for the operating system and anything else running on the workstation to avoid resource contention\.
+ **Browser**—The latest three versions of Google Chrome or Mozilla Firefox
+ **Network**—100 Kbps bandwidth per connected workstation
+ **Memory**—2 GB RAM
+ **Processor \(CPU\)**—2 GHz

#### Monitoring Workstations<a name="monitor-workstation"></a>

There are many factors that can affect CCP functionality at the workstation level\. Access to various levels of logging information is essential in determining steps towards remediation\. Adding additional logging and monitoring to workstations that are experiencing resource contention may further reduce available resources and invalidate test results\. We recommended that your workstation meet the minimum requirements outlined in the [Agent Workstation Requirements](#ccp-agent-hardware) section of this guide, leaving additional resources available for logging, monitoring, malware scanning, operating system functions, and any other running processes\.

Collect additional historical logging and data sources for correlation\. If you see a correlation between the time of the event and the time the issue was reported, you may be able to determine the root cause with the following information:
+ Round trip time \(RTT\) and packet loss to endpoints located within your Amazon Connect Region from your agent workstation, or an identical workstation on the same network segment\. If no Region endpoints are available because of security policies, any public WAN endpoint suffices, for example, www\.Amazon\.com\. Ideally, use your instance alias address \(https://yourInstanceName\.awsapps\.com\), and also your signaling address for endpoints\.
+ Regular monitoring of workstations that show processes running, and the current resource usage of each process\.
+ Workstation performance/utilization in these areas:
  + Processor \(CPU\)
  + Disk / drive
  + RAM / memory
  + Network throughput and performance
+ Monitor all of the preceding for your VDI desktop environment, including RTT/packet monitoring between the agent workstation and the VDI environment\.

### Network Ports and Protocols<a name="ccp-networking"></a>

The CCP soft phone requires three connections to AWS resources\. You must open the address and port to these resources with the appropriate protocol for the Region in which you created your Amazon Connect instance to allow bi\-directional communication for full functionality of the CCP\. The CCP needs access to the IP ranges for Amazon Elastic Compute Cloud \(Amazon EC2\) , Amazon CloudFront, and Amazon Connect, which are listed in the [https://ip\-ranges\.amazonaws\.com/ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json) file under Amazon EC2 \(EC2\), CloudFront \(CLOUDFRONT\), and Amazon Connect \(AMAZON\_CONNECT\) respectively\. The address ranges in the file are updated as new resources are added\. This means that you need to monitor the included ranges and update your environment accordingly to ensure that agents can use the CCP successfully\. 30 days after new IP ranges are added to this file, they start being used by Amazon Connect\.


| Service | Port | Protocol | Comments | 
| --- | --- | --- | --- | 
| Amazon Connect | 3478 | UDP in/out | Used for media endpoints within the Region, and for call audio for the softphone client\. | 
| Amazon Connect | 443 | TCP in/out |  | 
| Amazon EC2 | 443 | TCP in/out | CCP signaling endpoint | 
| CloudFront | 443 | TCP in/out | Used for hosting web content associated with your instance\. Endpoints are determined by the location of the end\-user client\. | 

Alternatively, for Amazon EC2 endpoints, you can allow access for the following URL and port to allow all Amazon EC2 endpoints rather than all of the IP Address ranges listed in the AWS ipranges\.json file:

`rtc.connect-telecom.{region}.amazonaws.com:443`

Replace `{region}` with the Region in which you created your Amazon Connect instance, such as `us-east-1`\. In certain proxy applications, web socket handling may impact functionality when using this address\. You should perform testing to validate before deploying to a production environment\.

For CloudFront, you can use the following URL with port 443 to allow traffic for all CloudFront endpoints\. Do this instead of including all ranges listed in the AWS ipranges\.json file: `https://myInstanceName.awsapps.com`\. Replace **myInstanceName** with the name of the instance for which to allow traffic\. In certain proxy applications, web socket handling may impact functionality when using this address, so you should perform testing to validate before deploying to a production environment\.

#### Port and Protocol Considerations<a name="port-considerations"></a>

Consider the following when implementing your network configuration changes for Amazon Connect:
+ You need to allow traffic for all addresses and ranges for the Region in which you created your Amazon Connect instance\.
+ If you are using a proxy or firewall between the CCP and Amazon Connect, increase the SSL certificate cache timeout to cover the duration of an entire shift for your agents, Do this to avoid connectivity issues with certificate renewals during their scheduled working time\. For example, if your agents are scheduled to work 8 hour shifts that include breaks, increase the interval to 8 hours plus time for breaks and lunch\.
+ When opening ports, Amazon EC2 and Amazon Connect require only the ports for endpoints in the same Region as your instance\. CloudFront, however, requires the endpoints in the Region closest to where your agents are located\. If you have agents in multiple Regions, you need to allow traffic for the endpoints in each Region where agents are using the Amazon Connect CCP\. For example, if your instance is US East, and you have an agent physically located in another country, you would need to open the ports for AWS CloudFormation using the IP address ranges for the Region where the agent is located\.
+ Update the ranges for which traffic is allowed within the 30 days after the ranges are updated in the [AWS ipranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json) file\. If you don't, you may experience intermittent connectivity issues when using the CCP with a softphone when traffic is routed to the new ranges, but not allowed to connect to your agents using the CCP\.
+ If you are using a custom CCP with the Amazon Connect Streams API, you can create a media\-less CCP that does not require opening ports for communication with Amazon Connect, but still requires ports opened for communication with Amazon EC2 and CloudFront\.

#### Region Selection Considerations<a name="ccp-region-selection"></a>

Amazon Connect Region selection is contingent upon data governance requirements, use case, services available in each Region, and latency in relation to your agents, callers, and external transfer endpoint geography\.
+ **Agent location/network**—CCP connectivity traverses the public WAN, so it is important that the workstation has the lowest latency and fewest hops possible, specifically to the AWS Region where your resources and Amazon Connect instance are hosted\. For example, hub and spoke networks that need to make several hops to reach an edge router can add latency and reduce the quality of experience\.

  When you set up your instance and agents, make sure to create your instance in the Region that is geographically closest to the Region where you create your instance\. If you need to set up an instance in a specific Region to comply with company policies or other regulations, choose the configuration that results in the fewest network hops between your agent computers and your Amazon Connect instance\.
+ **Location of your callers**—Because calls are anchored to your Amazon Connect Region endpoint, they are subject to PSTN latency\. Ideally your callers and transfer endpoints are geographically located as closely as possible to the AWS Region where your Amazon Connect instance is hosted for lowest latency\.

  For optimal performance, and to limit the latency for your customers when they call in to your contact center, create your Amazon Connect instance in the Region that is geographically closest to where your customers call from\. You might consider creating multiple Amazon Connect instances, and providing contact information to customers for the number that is closest to where they call from\.
+ **External transfers**—from Amazon Connect remain anchored to your Amazon Connect Region endpoint for the duration of the call\. Per\-minute usage continues to accrue until the call is disconnected by the recipient of the transferred call\. The call is not recorded after the agent drops or the transfer completes\. The CTR data and associated call recording of a transferred call are generated after the call is terminated\. Whenever possible, don't transfer calls that could be transferred back into Amazon Connect, known as circular transfers, to avoid compounding PSTN latency\.

#### Agents Using Amazon Connect Remotely<a name="remote-agents"></a>

Remote agents, those that use Amazon Connect from a location other than those connected to your organization's main network, may experience issues relating to their local network if they have an unstable connection, packet loss, or high latency\. This is compounded if a VPN is required to access resources\. Ideally, the agents are located close to the AWS Region where your AWS resources and Amazon Connect instance are hosted, and have a stable connection to the public WAN\.

#### Rerouting Audio<a name="reroute-audio"></a>

When rerouting audio to an existing device, consider the location of the device in relation to your Amazon Connect Region\. This is so you can account for potential additional latency\. If you reroute your audio, whenever there is a call intended for the agent, an outbound call is placed to the configured device\. When the agent answers the device, that agent is connected with the caller\. If the agent does not answer their device, they are moved into a missed call state until they or a supervisor changes their state back to available\.

#### Using AWS Direct Connect<a name="using-directconnect"></a>

AWS Direct Connect can help solve for latency and poor call quality between your edge router and AWS resources\. It also allows you to configure your edge router to redirect AWS traffic across dedicated fiber rather than traversing the public WAN\. This allows for a durable, consistent connection rather than relying on your ISP to dynamically route requests to AWS resources\. Keep in mind that this does not solve issues with the private LAN/WAN traversal to your edge router like hub\-and\-spoke network architecture\.

### Using Amazon Connect in a VDI Environment<a name="using-ccp-vdi"></a>

Virtual Desktop Infrastructure \(VDI\) environments add another layer of complexity to your solution that warrants separate POC efforts and performance testing to optimize\. The Amazon Connect Contact Control Panel \(CCP\) can operate in thick, thin, and zero client VDI environments as any other WebRTC based browser application does, and the configuration/support/optimization is best handled by your VDI support team\. That being said, the following is a collection of considerations and best practices that have been helpful for our VDI\-based customers\.
+ **Location of your agents**—Ideally, there are as few hops as possible with the lowest round trip time between the location from which your agents use the CCP and the VDI host location\.
+ **Host location of your VDI solution**—Ideally, your VDI host location is on the same network segment as your agents, with as few hops as possible from both internal resources as well as an edge router\. You also want the lowest round\-trip time possible to both WebRTC and Amazon EC2 range endpoints\.
+ **Network**—Each hop that traffic goes through between endpoints increases the possibility of failure and adds opportunity to introduce latency\. VDI environments are particularly susceptible to call quality issues if the underlying route is not optimized or the pipe isn't either fast or wide enough\. While AWS Direct Connect can improve call quality from the edge router to AWS, it will not address internal routing issues\. You may need to upgrade or optimize your private LAN/WAN, or redirect to an external device to circumvent call audio issues\. In most scenarios, if this is required, the CCP is not the only application that is having issues\.
+ **Dedicated resources**—at the Network and desktop level are recommended to prevent an impact to available agent resources from activities, such as backups and large file transfers\. One way to prevent resource contention is by restricting the desktop access to Amazon Connect users who will be using their environment similarly, instead of sharing resources with other business units who may use those resources differently\.
+ **Using a soft phone with remote connections**—in VDI environments can cause impact to audio quality\. If your agents connect to a remote endpoint and operates in that environment, we recommend either rerouting audio to an external E\.164 endpoint or connecting the media through the local device and then signaling through the remote connection\. You can build a custom CCP with the Amazon Connect Streams API by creating a CCP with no media for call signaling\. This way, the media is handled on the local desktop using standard CCP, and the signaling and call controls are handled on the remote connection with the CCP with no media\. For more information about the streams API, see the GitHub repository at [https://github\.com/aws/amazon\-connect\-streams](https://github.com/aws/amazon-connect-streams)\.

### CCP Connectivity<a name="ccp-connectivity"></a>

When an agent logs in, the CCP attempts to connect to the Amazon EC2 signaling endpoints listed in the AWS ipranges\.json file, Amazon Connect for media, and CloudFront for web artifacts such as images\. When the agent logs out or the browser is closed, endpoints are reselected when the agent next logs in\. If a connection to Amazon EC2 or Amazon Connect fails, errors display on the CCP\. If a connection to CloudFront fails, web elements such as buttons and icons, or even the page itself fails to load correctly\.

**Outbound calls:**
+ When an outbound call is placed, the event signal is sent to the Amazon EC2 endpoint, which then communicates with Amazon Connect to place the call\. Upon a successful dial attempt, the agent is bridged in, which anchors the call to the agent's Amazon Connect endpoint\. Any external transfers or conferences also uses the anchor until the call is disconnected\. Anchoring can help reduce PSTN latency\.

**Inbound calls:**
+ When an inbound call is received, the call is anchored to an Amazon Connect endpoint\. Any external transfers or conferences also use this anchor until the call is disconnected\.
+ When an agent is available, the call is pushed through via a new Amazon EC2 connection to their browser and offered to the agent\.
+ When the agent accepts the call and either the external device has been answered or the CCP determines it can receive a call, a connection to Amazon Connect is established for call media to the agent\.

**Transferred calls:**
+ When a call is transferred, the transfer event that signals to place an outbound call to the specified transfer destination is sent to Amazon EC2, which then communicates with Amazon Connect to place the call\.
+ When the call is connected, the agent is bridged in, anchoring the call to the agent's existing Amazon Connect endpoint\. Any external transfers or conferences also use this anchor until the call is disconnected\.
+ If the agent hangs up after the call is bridged, the agent's connection to the call is terminated, but Amazon Connect hangs on to the call at the Amazon Connect anchor point until there is a far side disconnect\. When the call is disconnected, CTRs and associated recordings are generated and made available for the call\.

**Missed calls:**
+ If the call is waiting on an agent, customer queue flow logic is used until an agent is available and the call has been successfully routed to that agent\.
+ If the agent does not accept the call, the agent moves into a Missed Call state and is unable to take calls until the agent, or a call center manager, changes their status to Available again\. The caller does not hear ringing while the call is waiting for the agent, and continues to hold until connected with an agent as defined in the customer queue flow logic\. 

**Panic logout:**
+ If the browser window where the CCP is running is closed, the call remains connected, but opening the browser and logging back in will not allow you to re\-establish the media connection\. You are still able to transfer or end the call, but no audio path is established between the agent and caller\.

## Troubleshooting Issues with the CCP<a name="trb-ccp"></a>

Troubleshooting CCP issues requires support from your network operations, system administrator, and VDI solution teams to collect the appropriate level of information to identify root cause and drive resolution\. To help determine the appropriate resources to engage, it's important to break issues down into those with similar symptoms\. The following guidance has been helpful in assisting Amazon Connect customers in resolving CCP issues with their operations support teams\.

**Topics**
+ [Common CCP Issues](#common-ccp-issues)
+ [Useful Troubleshooting Tools and Information](#tools-and-info)
+ [Gathering Helpful Information using the Streams API](#info-gathering)
+ [Analyzing the Data](#analyze-data)

### Common CCP Issues<a name="common-ccp-issues"></a>

The following are common issues encountered when using the Amazon Connect CCP\.
+ **CCP does not initialize/connect**—The most common causes are missing port/IP whitelist entries, not allowing browser microphone access, or not answering your external device\. Be sure that you have whitelisted all IPs covered in the [Network Ports and Protocols](#ccp-networking) section of this guide, and that you have allowed microphone access to your browser when prompted\.
+ **Periodic connection errors**—The most common cause is network contention, or there may have been an ipranges\.json update and the new entries have not been whitelisted\. For more information, see the [Network Ports and Protocols](#ccp-networking) section of this guide\.
+ **Missed calls, state change delays, and CCP unresponsive**—In most cases, this is intermittent and directly correlated with resource contention in the agent's workstation, network, or both\. This can be made worse, or caused directly, by a poor, unstable, or strained connection to AWS resources at the private WAN/LAN, public WAN levels, or local workstation resource contention\.

The following are common issues with call quality when using the CCP\. Call quality encompasses a large range of potential causes and is best approached by first identifying the types of issues that you're having\.
+ **Latency/cross\-talk**—in a voice connection manifests as a delay between when something is said and when the person on the other end hears it\. In some use cases that require a lot of conversation, high latency can create situations in which both parties are talking over each other\. The PSTN and agent latency need to be calculated in this scenario to identify contributing factors and take action to reduce PSTN latency, agent latency, or both\. For more information, see the PSTN and agent connection latency section of this documentation\.
+ **One way audio**—is when the agent can't hear the caller or the caller can't hear them\. This is normally indicative of an issue with the agent's workstation at the hardware, network, resource levels, or all three\. It and can also be related to browser microphone permissions or headset issues\. For more information, see the [Monitoring Workstations](#monitor-workstation) section of this guide\.
+ **Volume increase or decrease**— can happen at the beginning or intermittently during the call, and it's important to differentiate the two for troubleshooting purposes\. Typically, this relates to forwarding calls to or from Amazon Connect that inherit this from an issue with the third party transfer\.
+ **Audio choppy, cutting out, echo, reverb, or other signal noise**—could also manifest as a robotic sound or other distortion making it difficult for either the agent, caller, or both parties to understand what’s being said\. This is normally indicative of an issue with the agent's workstation at the hardware, network, resource levels, or all three\. For more information, see the [Monitoring Workstations](#monitor-workstation) section of this guide\.
+ **Wobble**—is the effect that media codecs can have on audio that manifests as the slowing down and speeding up of audio to combat high jitter and latency\. This is normally indicative of an issue with the agent's workstation at the hardware, network, resource levels, or all three\. For more information, see the [Monitoring Workstations](#monitor-workstation) section of this guide\.
+ **Disconnects**—can happen at any point in the call\. It is important to note when during the call that the disconnections occur to identify a pattern\. For example, disconnects on call transfers to a specific external number typically relate to forwarding calls to or from Amazon Connect that inherit this from an issue with the third party transfer\. They can also be related to circular transfers, which means transferring calls out of Amazon Connect and back in the same call\.

### Useful Troubleshooting Tools and Information<a name="tools-and-info"></a>

The following tools and information can be helpful with troubleshooting issues with Amazon Connect\.
+ **Instance ARN**—Provide your instance ARN when you contact AWS support so that they can see the activity in your Amazon Connect instance\. You can find the ARN for your instance on the Overview page that you access by choosing the alias of the instance from the Amazon Connect console\.
+ **Call recordings**—are very useful, not only to illustrate and determine reported behavior, but also to rule out audio issues from the agent's side\. Recordings in Amazon Connect are done at the instance side of the interaction, before the audio traverses the agent connection\. This allows you to determine if the audio issue was isolated to the agent's side of the interaction or if it existed in the audio received by the agent\. You can find call recordings associated with a contact in the Contact Search report\.
+ **Contact IDs from the CTR**—Provide when you contact AWS support\.
+ **Agent desktop performance/process logs**—can help rule out local resource/network contention\.
+ **Contact Control Panel logs**—to track agent actions and timing\. To download CCP logs, choose the settings cogwheel in the CCP, and then choose **Download logs**\. The logs are saved to your browser's default download directory\.
+ **Network utilization logging/monitoring**—specifically for latency and dropped packets on the same network segment as your agents\.
+ **Private WAN/LAN network diagram**—outlining connection paths to the edge router to AWS to explain network traversal\.
+ **Firewall whitelist access**—to verify that IP/port ranges are whitelisted as described in [Network Ports and Protocols](#ccp-networking)\.
+ **Audio capturing and analytic tools**—for latency calculations from the agent's workstation\.
+ **AWS region latency test tools**—such as the [Amazon Connect Call Control Panel Connectivity Tool](https://s3.amazonaws.com/connectivitytest/checkConnectivity.html)\.

### Gathering Helpful Information using the Streams API<a name="info-gathering"></a>

For tracking and troubleshooting issues at scale, collecting data surrounding overall call quality is recommended\. Anytime poor call quality is experienced, agents can note the current time and corresponding disposition code by using the disposition key chart, as shown in the following chart\. Alternatively, you can use the Streams API to incorporate your own report and issue feature in the custom CCP to write these dispositions with corresponding call information to a database, like Amazon DynamoDB\. For more information about the Amazon Connect Streams API, see the GitHub repository at [https://github\.com/aws/amazon\-connect\-streams](https://github.com/aws/amazon-connect-streams)\.

### Example Agent Issue Report Disposition<a name="streams-disp-keys."></a>

The following example disposition keys are listed by symptom, scenario, and severity\.

**Symptom**
+ **S**—Softphone error
+ **M**—Missed calls
+ **L**—Latency causes poor quality
+ **P**—Starts off OK, gets progressively worse over time
+ **D**—Disconnected calls
+ **W**—One way audio; for example, the agent can hear the customer, but the customer cannot hear the agent
+ **V**—Volume too quiet or too loud
+ **C**—Choppy/cuts in and out intermittently

**Scenario**
+ **O**—Outbound call
+ **I**—Inbound call
+ **T**—Three\-way call

**Severity**
+ **1**—Small impact, but can use the CCP effectively
+ **2**—Medium impact, communication is difficult, but can still service calls
+ **3**—Large impact, cannot use the CCP to take calls

For example:
+ 5:45PM agentName LT2 \(latency on a three\-way call with medium impact\)\.
+ 6:05PM agentName DO3 \(disconnected three\-way call with large impact\)\.
+ 6:34PM agentName MI3 \(missed inbound call with large impact\)\.

### Analyzing the Data<a name="analyze-data"></a>

The following guidelines can assist you in analyzing the data to identify issues in your environment\.
+ Use the CTR / Contact search report to identify the contact IDs for the contacts during which call quality issues occurred\. The CTR includes a link to the associated call recording, and additional details that you can use for symptom verification and to provide to your AWS support representative\.
+ Use the agent name and timestamp in the CTR to get a sense of the types of issues you're experiencing and their prevalence by agent, symptom, scenario, and severity over time\. This will allow you to see if issues are happening around the same time, surround a specific event, or are isolated to specific agents or agent actions\. You can also easily identify and access associated call recordings and associated contact IDs available if you need to engage support\.
+ Correlate data sources, such as local network logs, CPU/disk/memory utilization and process monitor logs from the operating system on the client workstation\. This lets you correlate events by agent over time to rule out local resource contention as a cause or contributor\.
+ Analyze data by symptom and scenario reported per minute or per hour to create heat maps of an issue by type and severity by agent over time\. Doing this is especially helpful in environmental troubleshooting as you may find clustered impacts associated with scheduled activity like backups or large file transfers\.
+ If you can't find any evidence of local resource contention or derive any noteworthy correlations, you can use the contact IDs collected to open a support case\. If issues experienced are intermittent in nature, they most likely relate to issues with the agent's workstation, network connectivity, or both\.

## Validation Testing<a name="valid-testing"></a>

Voice quality issues can have many contributing sources\. It's important to run controlled tests and monitor the same environment or workstation as those reporting the issue, and be able to reproduce the same use cases\. Consider the following general testing recommendations for measuring and gathering data to investigate voice quality issues\.

### PSTN and Agent Connection Latency<a name="pstn-agent-latency"></a>

For troubleshooting cross\-talk issues, you need to differentiate and measure agent and raw PSTN latency contributions, as they require different remediation efforts\.
+ \[overall\_latency\] is the total latency experienced between caller and agent\. This latency can be calculated as \[overall\_latency\] = \[agent\_latency\] \+ \[pstn\_latency\]\.
+ \[pstn\_latency\] is the latency between Amazon Connect endpoint and the caller\. This latency can be calculated as \[pstn\_latency\] = \[overall\_latency\] \- \[agent\_connection\_latency\]\. This latency can be improved by using a different Amazon Connect Region location or avoiding external and circular transfers to geographically distant endpoint locations\.
+ \[agent\_latency\] is the latency between Amazon Connect endpoint and the agent\. This latency can be calculated as \[agent\_latency\] = \[overall\_latency\] \- \[recording\_latency\]\. This latency can be improved by using AWS Direct Connect for agents on\-premises, avoiding the use of VPN connections, improving private WAN/LAN performance/durability, or using an Amazon Connect Region location closer to your agents\. Depending on your use case, selecting a different Region selection may also increase \[pstn\_latency\]\.
+ \[redirect\_latency\] is the latency resulting in redirecting audio to an external device\. This latency can be calculated by measuring \[overall\_latency\] once with redirect and once without and take the difference between the two\.
+ \[forward\_latency\] is the latency resulting in forward calls to or from Amazon Connect\. This latency can be calculated by measuring \[overall\_latency\], once with forward and once without, and take the difference between the two\.

#### Measuring Latency<a name="measure-latency"></a>
+ Reproduce your use case\. Any deviations need to be measured and accounted for, because they skew test results\.
+ Match production controls and environment as much as possible\. Use the same flows, phone numbers, and endpoint locations\.
+ Note the geographical locations of your callers, agents, and external transfer destinations, where applicable\. If you are servicing multiple countries, each country should be tested individually to provide the same test coverage that your agents experience in production\.
+ Note mobile and land line use in your tests\. Mobile networks can add latency and need to be measured and considered for customer, agent, and transfer endpoints, where applicable\.
+ Reproduce the business use case\. If the agents use conference and transfer, be sure to test those scenarios\. If circular transfers occur, which are not recommended, be sure to test those as well\.
+ Reproduce the agent environment by including the workstation environment, located on the same network segment, and using equipment your agents would use\.

#### Requirements for Testing Latency<a name="test-reqs-latency"></a>

To perform effective testing for latency, the following are required:
+ Call recording enabled to capture \[agent\_latency\]\. Without call recording, you can calculate only \[overall\_latency\]\.
+ A customer phone source\. For testing, confirm call quality on an actual call from a customer\.
+ An agent phone, if redirecting audio to an external device\. You must be able to record the input and output of this device\.
+ A third\-party transfer endpoint, if applicable\. Testing is best when performed on actual calls or transfers from a third party\.
+ An agent workstation with sound recording or analysis software\.
+ Reproducible use cases\. Troubleshooting can be difficult for issues that cannot be reproduced\.
+ NTP or other method to sync timestamps to facilitate identifying specific contacts and when they occurred, especially when activity is occurring across multiple time zones\.

#### Testing Inbound Calls Using a Soft Phone<a name="inbound-test-plan"></a>

This process allows you to complete a latency test scenario in \~15 seconds\. Analyzing the results and marking timestamps takes approximately 1\-2 minutes per recording\.

1. Go to a quiet location\.

1. Configure agent workstation to play audio from external speakers and make sure they are turned up\.

1. Use the agent workstation to log in to the CCP\.

1. Start recording using an audio capturing tool on the agent workstation\.

1. From the customer's phone source, use a speaker phone to call the incoming number for your Amazon Connect instance\. This could really just be any external phone source to simulate a customer call\.

1. Answer the incoming call using the soft phone on the agent workstation\.

1. Make sure that the customer phone is not muted\.

1. On the customer side, use an object or your hand, tap loudly on the desk or table, and then immediately mute the customer phone\.

1. Wait 3 or more seconds\. Repeat steps 7\-8 at least 3 times\.

1. Stop recording on the agent workstation\.

1. Open the recording in your audio analysis tool\. You should be able to see both the initial tapping sound that you made on the desk, and the tapping sound on the agent line on the other end\. Take the three deltas and average for your \[overall\_latency\]\.

1. Optionally, to calculate \[agent\_latency\], open the associated Amazon Connect call recording in your audio analysis tool\. You should be able to see both the initial tapping sound and the sound when it arrives to the agent at the other end\. Take the three deltas and average for your \[recording\_latency\]\. \[agent\_latency\] = \[overall\_latency\] \- \[recording\_latency\]\. Repeat as needed\. 

Modify the test plan as necessary to fit your use case\. As the steps change, the process of recording and analyzing the audio is the same\. If you need to test conferences and transfers, take measurements as normal, and then take another measurement when the conference is active with the third party transfer endpoint\.

#### Interpreting the Test Results<a name="interpret-results"></a>

The impact of increasing \[overall\_latency\] begins to be noticeable at approximately 300ms and can result in crosstalk above 500ms\. The impact, and what level of latency is considered acceptable, depends on your use case\. For recommended remediation efforts for decreasing latency, see the [PSTN and Agent Connection Latency](#pstn-agent-latency)\.
