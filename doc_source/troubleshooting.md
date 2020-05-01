# Troubleshooting Issues with the CCP<a name="troubleshooting"></a>

Troubleshooting CCP issues requires support from your network operations, system administrator, and VDI solution teams to collect the appropriate level of information to identify root cause and drive resolution\. To help determine the appropriate resources to engage, it's important to break issues down into those with similar symptoms\. The following guidance has been helpful in assisting Amazon Connect customers in resolving CCP issues with their operations support teams\.

**Topics**
+ [Use the Check Connectivity Tool](#check-connectivity-tool)
+ [Common CCP Issues](#common-ccp-issues)
+ [Useful Troubleshooting Tools and Information](#tools-and-info)
+ [Gathering Helpful Information using the Streams API](#info-gathering)
+ [Analyzing the Data](#analyze-data)
+ [Validation Testing](#valid-testing)

## Use the Check Connectivity Tool<a name="check-connectivity-tool"></a>

When your agents are experiencing problems with CCP, we recommend you go to their workstation and run the [Amazon Connect Check Connectivity Tool](https://s3.amazonaws.com/connectivitytest/checkConnectivity.html)\. 

This tool will check which web browser the agent is running, and whether the microphone has required permissions\. Click the **Test** buttons to check the ports and latency\. 

## Common CCP Issues<a name="common-ccp-issues"></a>

The following are common issues encountered when using the Amazon Connect CCP\.
+ **CCP does not initialize/connect**—The most common causes are missing port/IP allow list entries, not allowing browser microphone access, or not answering your external device\. Be sure that you have added to the allow list all IPs covered in the [Set Up Your Network](ccp-networking.md) section of this guide, and that you have allowed microphone access to your browser when prompted\.
+ **Periodic connection errors**—The most common cause is network contention, or there may have been an ipranges\.json update and the new entries have not been added to the allow list\. For more information, see the [Set Up Your Network](ccp-networking.md) section of this guide\.
+ **Missed calls, state change delays, and CCP unresponsive**—In most cases, this is intermittent and directly correlated with resource contention in the agent's workstation, network, or both\. This can be made worse, or caused directly, by a poor, unstable, or strained connection to AWS resources at the private WAN/LAN, public WAN levels, or local workstation resource contention\.

The following are common issues with call quality when using the CCP\. Call quality encompasses a large range of potential causes and is best approached by first identifying the types of issues that you're having\.
+ **Latency/cross\-talk**—in a voice connection manifests as a delay between when something is said and when the person on the other end hears it\. In some use cases that require a lot of conversation, high latency can create situations in which both parties are talking over each other\. The PSTN and agent latency need to be calculated in this scenario to identify contributing factors and take action to reduce PSTN latency, agent latency, or both\. For more information, see the PSTN and agent connection latency section of this documentation\.
+ **One way audio**—is when the agent can't hear the caller or the caller can't hear them\. This is normally indicative of an issue with the agent's workstation at the hardware, network, resource levels, or all three\. It and can also be related to browser microphone permissions or headset issues\. For more information, see the [Monitoring Workstations](ccp-agent-hardware.md#monitor-workstation) section of this guide\.
+ **Volume increase or decrease**— can happen at the beginning or intermittently during the call, and it's important to differentiate the two for troubleshooting purposes\. Typically, this relates to forwarding calls to or from Amazon Connect that inherit this from an issue with the third party transfer\.
+ **Audio choppy, cutting out, echo, reverb, or other signal noise**—could also manifest as a robotic sound or other distortion making it difficult for either the agent, caller, or both parties to understand what’s being said\. This is normally indicative of an issue with the agent's workstation at the hardware, network, resource levels, or all three\. For more information, see the [Monitoring Workstations](ccp-agent-hardware.md#monitor-workstation) section of this guide\.
+ **Wobble**—is the effect that media codecs can have on audio that manifests as the slowing down and speeding up of audio to combat high jitter and latency\. This is normally indicative of an issue with the agent's workstation at the hardware, network, resource levels, or all three\. For more information, see the [Monitoring Workstations](ccp-agent-hardware.md#monitor-workstation) section of this guide\.
+ **Disconnects**—can happen at any point in the call\. It is important to note when during the call that the disconnections occur to identify a pattern\. For example, disconnects on call transfers to a specific external number typically relate to forwarding calls to or from Amazon Connect that inherit this from an issue with the third party transfer\. They can also be related to circular transfers, which means transferring calls out of Amazon Connect and back in the same call\.

## Useful Troubleshooting Tools and Information<a name="tools-and-info"></a>

The following tools and information can be helpful with troubleshooting issues with Amazon Connect\.
+ **Instance ARN**—Provide your instance ARN when you contact AWS support so that they can see the activity in your Amazon Connect instance\. You can find the ARN for your instance on the Overview page that you access by choosing the alias of the instance from the Amazon Connect console\.
+ **Call recordings**—are very useful, not only to illustrate and determine reported behavior, but also to rule out audio issues from the agent's side\. Recordings in Amazon Connect are done at the instance side of the interaction, before the audio traverses the agent connection\. This allows you to determine if the audio issue was isolated to the agent's side of the interaction or if it existed in the audio received by the agent\. You can find call recordings associated with a contact in the Contact Search report\.
+ **Contact IDs from the CTR**—Provide when you contact AWS support\.
+ **Agent desktop performance/process logs**—can help rule out local resource/network contention\.
+ **Contact Control Panel logs**—to track agent actions and timing\. To download CCP logs, choose the settings cogwheel in the CCP, and then choose **Download logs**\. The logs are saved to your browser's default download directory\.
+ **Network utilization logging/monitoring**—specifically for latency and dropped packets on the same network segment as your agents\.
+ **Private WAN/LAN network diagram**—outlining connection paths to the edge router to AWS to explain network traversal\.
+ **Firewall allow list access**—to verify that IP/port ranges are added to the allow list \(also known as whitelist\) as described in [Set Up Your Network](ccp-networking.md)\.
+ **Audio capturing and analytic tools**—for latency calculations from the agent's workstation\.
+ **AWS region latency test tools**—such as the [Amazon Connect Call Control Panel Connectivity Tool](https://s3.amazonaws.com/connectivitytest/checkConnectivity.html)\.

## Gathering Helpful Information using the Streams API<a name="info-gathering"></a>

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

**Examples**
+ 5:45PM agentName LT2 \(latency on a three\-way call with medium impact\)\.
+ 6:05PM agentName DO3 \(disconnected three\-way call with large impact\)\.
+ 6:34PM agentName MI3 \(missed inbound call with large impact\)\.

## Analyzing the Data<a name="analyze-data"></a>

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

  Amazon Connect leverages CloudFront for connectivity\. Not all CloudFront ranges are advertised over AWS Direct Connect\. This means not all URLs generated by AWS Direct Connect are reachable over a Public Virtual Interface\. 
+ \[redirect\_latency\] is the latency resulting in redirecting audio to an external device\. This latency can be calculated by measuring \[overall\_latency\] once with redirect and once without and take the difference between the two\.
+ \[forward\_latency\] is the latency resulting in forward calls to or from Amazon Connect\. This latency can be calculated by measuring \[overall\_latency\], once with forward and once without, and take the difference between the two\.

#### Measuring Latency<a name="measure-latency"></a>

In addition to the steps below, see [Measure latency for validation testing and troubleshooting in Amazon Connect\)](https://aws.amazon.com/blogs/contact-center/measure-latency-for-validation-testing-and-troubleshooting-in-amazon-connect/)\.
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

This process allows you to complete a latency test scenario in about 15 seconds\. Analyzing the results and marking timestamps takes approximately 1\-2 minutes per recording\.

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