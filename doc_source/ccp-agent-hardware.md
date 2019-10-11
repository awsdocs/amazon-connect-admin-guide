# Agent Workstation Requirements for the CCP<a name="ccp-agent-hardware"></a>

Agent workstations in the contact center vary widely\. While the Amazon Connect CCP is built to handle high levels of jitter and high latency environments, the architecture of the workstations that agents use, and the location and environment in which they take contacts, can impact the quality of experience\.

Under\-powered workstations can make it difficult for agents to access the tools and resources they need to service contacts\. Also, keep in mind the resource requirements when scoping workstations to ensure that they can perform under load while appropriately multitasking for the use case\. For the best agent and customer audio experience, a USB headset is recommended\. Alternatively, you can redirect the contact to an external number, in E\.164 format, using an agent's existing telephony\.

 The following values are the minimum system requirements for the workstations using the CCP only\. Additional memory, bandwidth, and CPU should be scoped for the operating system and anything else running on the workstation to avoid resource contention\.
+ **Browser**—The latest three versions of Google Chrome or Mozilla Firefox
+ **Network**—100 Kbps bandwidth per connected workstation
+ **Memory**—2 GB RAM
+ **Processor \(CPU\)**—2 GHz

## Monitoring Workstations<a name="monitor-workstation"></a>

There are many factors that can affect CCP functionality at the workstation level\. Access to various levels of logging information is essential in determining steps towards remediation\. Adding additional logging and monitoring to workstations that are experiencing resource contention may further reduce available resources and invalidate test results\. We recommended that your workstation meet the minimum requirements outlined in the [Agent Workstation Requirements for the CCPAgent Workstation Requirements](#ccp-agent-hardware) section of this guide, leaving additional resources available for logging, monitoring, malware scanning, operating system functions, and any other running processes\.

Collect additional historical logging and data sources for correlation\. If you see a correlation between the time of the event and the time the issue was reported, you may be able to determine the root cause with the following information:
+ Round trip time \(RTT\) and packet loss to endpoints located within your Amazon Connect Region from your agent workstation, or an identical workstation on the same network segment\. If no Region endpoints are available because of security policies, any public WAN endpoint suffices, for example, www\.Amazon\.com\. Ideally, use your instance alias address \(https://yourInstanceName\.awsapps\.com\), and also your signaling address for endpoints\.
+ Regular monitoring of workstations that show processes running, and the current resource usage of each process\.
+ Workstation performance/utilization in these areas:
  + Processor \(CPU\)
  + Disk / drive
  + RAM / memory
  + Network throughput and performance
+ Monitor all of the preceding for your VDI desktop environment, including RTT/packet monitoring between the agent workstation and the VDI environment\.