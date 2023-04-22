# Agent headset and workstation requirements for the CCP<a name="ccp-agent-hardware"></a>

Agent headsets and workstations in the contact center vary widely\. While the Amazon Connect CCP is built to handle high levels of jitter and high latency environments, the architecture of the **workstations** that agents use, and the location and environment in which they take contacts, can impact the quality of experience\.

## Headset requirements<a name="ccp-agent-headset"></a>

The agent's Contact Control Panel \(CCP\) is compatible with all types of headsets\.

For the best agent and customer experience, we recommend using a USB headset\.

Alternatively, you can redirect the contact to an external number, in E\.164 format, using an agent's existing telephony\.

**Note**  
If the agent's audio device does not support up to 48khz and the browser asserts a sample rate of 48khz, audio issues such as an audible humming sound may be present in the agent's outgoing audio\. This has been seen with Firefox but not with Chrome\.   
For instructions on verifying the sample rate of the agent's headset and browser, see [Humming sound in headset: Verify the headset and browser sample rates](verify-sample-rate.md)

## Workstation minimum requirements<a name="ccp-agent-workstation"></a>

Under\-powered workstations can make it difficult for agents to access the tools and resources they need to service contacts\. Also, keep in mind the resource requirements when scoping workstations to ensure that they can perform under load while appropriately multitasking for the use case\. 

Following are the minimum system requirements for the workstations using the CCP only\. You'll need to scope additional memory, bandwidth, and CPU for the operating system and anything else running on the workstation to avoid resource contention\.
+ **Browser**—For a list of all supported browsers, see [Browsers supported by Amazon Connect](connect-supported-browsers.md)\. 
+ **Network**—100 Kbps bandwidth per connected workstation
+ **Memory**—2 GB RAM
+ **Processor \(CPU\)**—2 GHz

## iPhone and other mobile devices are not supported<a name="ccp-iphone"></a>

The Amazon Connect console, Contact Control Panel \(CCP\), and agent workspace do not support mobile browsers\.

## How to determine whether a workstation is the source of problems<a name="monitor-workstation"></a>

To determine whether a workstation is the source of problems, you need access to various levels of logging information\. However, adding logging and monitoring to workstations that are already experiencing resource contention may further reduce available resources and invalidate test results\. We recommended that your workstation meet the minimum requirements, so you leave additional resources available for logging, monitoring, malware scanning, operating system functions, and any other running processes\.

Collect additional historical logging and data sources for correlation\. If you see a correlation between the time of the event and the time the issue was reported, you may be able to determine the root cause with the following information:
+ Round trip time \(RTT\) and packet loss to endpoints located within your Amazon Connect Region from your agent workstation, or an identical workstation on the same network segment\. If no Region endpoints are available because of security policies, any public WAN endpoint suffices, for example, www\.Amazon\.com\. Ideally, use your instance alias address \(https://yourInstanceName\.awsapps\.com\), and also your signaling address for endpoints\.

  You can find your Region endpoints here: [Amazon Connect endpoints and quotas](https://docs.aws.amazon.com/general/latest/gr/connect_region.html)\.
+ Regular monitoring of workstations that show processes running, and the current resource usage of each process\.
+ Workstation performance/utilization in these areas:
  + Processor \(CPU\)
  + Disk / drive
  + RAM / memory
  + Network throughput and performance
+ Monitor all of the preceding for your VDI desktop environment, including RTT/packet monitoring between the agent workstation and the VDI environment\.