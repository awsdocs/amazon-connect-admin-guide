# Set Up Your Network<a name="ccp-networking"></a>

Traditional VoIP solutions require you to allow both inbound and outbound for specific UDP port ranges and IPs, such as 80 and 443\. These solutions also apply to TCP\. In comparison, the network requirements for using the Contact Control Panel \(CCP\) with a softphone are less intrusive\. You can establish persistent outbound send/receive connections through your web browser\. As a result, you don't need to open a client\-side port to listen for inbound traffic\. 

The following diagram shows you what each port is used for\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/networking.png)

The following sections describe the two primary connectivity options for using the CCP\. 

## Option 1 \(Recommended\): Replace Amazon EC2 and CloudFront IP Range Requirements with a Domain Allow List<a name="option1"></a>

This first option lets you significantly reduce your blast radius\. 

We recommend trying Option 1 and testing it with more than 200 calls\. Test for softphone errors, dropped calls, and conference/transfer functionality\. If your error rate is greater than 2 percent, there might be an issue with proxy resolution\. If that's the case, consider using Option 2\. 


| IP\-Ranges entry | AWS Region | Ports/Protocols | Direction | Traffic | 
| --- | --- | --- | --- | --- | 
| AMAZON\_CONNECT | GLOBAL and Region where your Amazon Connect instance is located  \(GLOBAL only if a region\-specific entry doesn't exist\)  | 3478 \(UDP\) | OUTBOUND | SEND/RECEIVE | 

**Tip**  
If you don't see an entry for your region, use GLOBAL\. For example, there isn't an entry for ap\-southeast\-1, so you would use GLOBAL\.

To allow traffic for Amazon EC2 endpoints, allow access for the URL and port, as shown in the first row of the following table\. Do this instead of allowing all of the IP address ranges listed in the ip\-ranges\.json file\. You get the same benefit using a domain for CloudFront, as shown in the second row of the following table\.


| Domain/URL allow list | AWS Region | Ports | Direction | Traffic | 
| --- | --- | --- | --- | --- | 
| rtc\.connect\-telecom\.\{region\}\.amazonaws\.com Please see the note following this table\.  | Replace \{region\} with the Region where your Amazon Connect instance is located | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 
| \{myInstanceName\}\.awsapps\.com/connect/ccp \{myInstanceName\}\.awsapps\.com/connect/api\*\.cloudfront\.net  | Replace \{myInstanceName\} with the alias of your Amazon Connect instance | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 
| \*\.execute\-api\.\{region\}\.amazonaws\.com  | Replace \{region\} with the location of your Amazon Connect instance | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 
| participant\.connect\.\{region\}\. amazonaws\.com  | Replace \{region\} with the location of your Amazon Connect instance | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 
| \*\.transport\.connect\.\{region\}\. amazonaws\.com  | Replace \{region\} with the location of your Amazon Connect instance | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 

**Note**  
The new region telecom endpoints follow a different format\. Here's a complete list of telecom endpoints:  


| Region | Domain/URL | 
| --- | --- | 
| us\-west\-2  | rtc\.connect\-telecom\.us\-west\-2\.amazonaws\.com | 
| us\-east\-1  | rtc\.connect\-telecom\.us\-east\-1\.amazonaws\.com | 
| eu\-central\-1  | rtc\.connect\-telecom\.eu\-central\-1\.amazonaws\.com | 
| ap\-southeast\-2  | rtc\.connect\-telecom\.ap\-southeast\-2\.amazonaws\.com | 
| ap\-northeast\-1  | rtc\.connect\-telecom\.ap\-northeast\-1\.amazonaws\.com | 
| eu\-west\-2  | rtc\.cell\-1\.prod\.eu\-west\-2\.prod\.connect\.aws\.a2z\.com | 
| ap\-southeast\-1  | rtc\.cell\-1\.prod\.ap\-southeast\-1\.prod\.connect\.aws\.a2z\.com | 

**Tip**  
When using `rtc.connect-telecom.{region}.amazonaws.com` and `https://myInstanceName.awsapps.com`, in certain proxy applications, web socket handling may impact functionality\. Be sure to test and validate before deploying to a production environment\.

## Option 2 \(Not Recommended\): Allow IP Address Ranges<a name="option2"></a>

The second option relies on using an allow list, also known as whitelisting, the IP addresses used by Amazon Connect\. You create this allow list using the IP addresses in the [AWS ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json) file\. 

For more information about this file, see [About Amazon Connect IP Address Ranges](#about-connect-ip-address-range)\.


| IP\-Ranges entry | AWS Region | Ports/Protocols | Direction | Traffic | 
| --- | --- | --- | --- | --- | 
| AMAZON\_CONNECT | GLOBAL and Region where your Amazon Connect instance is located \(GLOBAL only if a region\-specific entry doesn't exist\) | 3478 \(UDP\) | OUTBOUND | SEND/RECEIVE | 
| EC2 | GLOBAL and Region where your Amazon Connect instance is located \(GLOBAL only if a region\-specific entry doesn't exist\) | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 
| CLOUDFRONT | Global\* | 443 \(TCP\) | OUTBOUND | SEND/RECEIVE | 

**Tip**  
If you don't see an entry for your region, use GLOBAL\. For example, there isn't an entry for ap\-southeast\-1, so you would use GLOBAL\.

\*CloudFront serves static content from an edge location that has the lowest latency in relation to where your agents are located\. IP range allow lists for CloudFront are global and require all IP ranges associated with **"service": "CLOUDFRONT"** in the ip\-ranges\.json file\. 

## About Amazon Connect IP Address Ranges<a name="about-connect-ip-address-range"></a>

In the [AWS ip\-ranges\.json](https://ip-ranges.amazonaws.com/ip-ranges.json) file, the whole /19 IP address range is owned by Amazon Connect\. All traffic to and from the /19 range comes to and from Amazon Connect\.

The /19 IP address range isn't shared with other services\. It's for the exclusive use to Amazon Connect globally\.

In the AWS ip\-ranges\.json file, you can see the same range listed twice\. For example: 

```
            
                { "ip_prefix": "15.193.0.0/19", 
                "region": "GLOBAL", 
                "service": "AMAZON" 
                }, 
                {
                "ip_prefix": "15.193.0.0/19", 
                "region": "GLOBAL", 
                "service": "AMAZON_CONNECT" 
                },
```

AWS always publishes any IP range twice: one for the specific service, and one for “AMAZON” service\. There could even be a third listing for a more specific use case within a service\. 

When there are new IP address ranges supported for Amazon Connect, they are added to the publicly available ip\-ranges\.json file\. They are kept for a minimum of 30 days before they are used by the service\. After 30 days, softphone traffic through the new IP address ranges increases over the subsequent two weeks\. After two weeks, traffic is routed through the new ranges equivalent to all available ranges\.

For more information about this file and IP address ranges in AWS, see [AWS IP Address Ranges](https://docs.aws.amazon.com/general/latest/gr/aws-ip-ranges.html)\.

## Stateless Firewalls<a name="stateless-firewalls"></a>

If you're using a stateless firewall for both options, use the requirements described in the previous sections\. Then you must add to your allow list the ephemeral port range used by your browser, as shown in the following table\. 


| IP\-Range entry | Port | Direction | Traffic | 
| --- | --- | --- | --- | 
| AMAZON\_CONNECT | 49152\-65535 \(UDP\) | INBOUND | SEND/RECEIVE | 

## Port and Protocol Considerations<a name="port-considerations"></a>

Consider the following when implementing your network configuration changes for Amazon Connect:
+ You need to allow traffic for all addresses and ranges for the Region in which you created your Amazon Connect instance\.
+ If you are using a proxy or firewall between the CCP and Amazon Connect, increase the SSL certificate cache timeout to cover the duration of an entire shift for your agents, Do this to avoid connectivity issues with certificate renewals during their scheduled working time\. For example, if your agents are scheduled to work 8 hour shifts that include breaks, increase the interval to 8 hours plus time for breaks and lunch\.
+ When opening ports, Amazon EC2 and Amazon Connect require only the ports for endpoints in the same Region as your instance\. CloudFront, however, serves static content from an edge location that has the lowest latency in relation to where your agents are located\. IP range allow lists for CloudFront are global and require all IP ranges associated with "service": "CLOUDFRONT" in ip\-ranges\.json\.
+ Once ip\-ranges\.json is updated, the associated AWS service will begin using the updated IP ranges after 30 days\. To avoid intermittent connectivity issues when the service begins routing traffic to the new IP ranges, be sure to add the new IP ranges to your allow list, within 30 days from the time they were added to ip\-ranges\.json\.
+ If you are using a custom CCP with the Amazon Connect Streams API, you can create a media\-less CCP that does not require opening ports for communication with Amazon Connect, but still requires ports opened for communication with Amazon EC2 and CloudFront\.

## Region Selection Considerations<a name="ccp-region-selection"></a>

Amazon Connect Region selection is contingent upon data governance requirements, use case, services available in each Region, and latency in relation to your agents, contacts, and external transfer endpoint geography\.
+ **Agent location/network**—CCP connectivity traverses the public WAN, so it is important that the workstation has the lowest latency and fewest hops possible, specifically to the AWS Region where your resources and Amazon Connect instance are hosted\. For example, hub and spoke networks that need to make several hops to reach an edge router can add latency and reduce the quality of experience\.

  When you set up your instance and agents, make sure to create your instance in the Region that is geographically closest to the Region where you create your instance\. If you need to set up an instance in a specific Region to comply with company policies or other regulations, choose the configuration that results in the fewest network hops between your agent computers and your Amazon Connect instance\.
+ **Location of your callers**—Because calls are anchored to your Amazon Connect Region endpoint, they are subject to PSTN latency\. Ideally your callers and transfer endpoints are geographically located as closely as possible to the AWS Region where your Amazon Connect instance is hosted for lowest latency\.

  For optimal performance, and to limit the latency for your customers when they call in to your contact center, create your Amazon Connect instance in the Region that is geographically closest to where your customers call from\. You might consider creating multiple Amazon Connect instances, and providing contact information to customers for the number that is closest to where they call from\.
+ **External transfers**—from Amazon Connect remain anchored to your Amazon Connect Region endpoint for the duration of the call\. Per\-minute usage continues to accrue until the call is disconnected by the recipient of the transferred call\. The call is not recorded after the agent drops or the transfer completes\. The CTR data and associated call recording of a transferred call are generated after the call is terminated\. Whenever possible, don't transfer calls that could be transferred back into Amazon Connect, known as circular transfers, to avoid compounding PSTN latency\.

## Agents Using Amazon Connect Remotely<a name="remote-agents"></a>

Remote agents, those that use Amazon Connect from a location other than those connected to your organization's main network, may experience issues relating to their local network if they have an unstable connection, packet loss, or high latency\. This is compounded if a VPN is required to access resources\. Ideally, the agents are located close to the AWS Region where your AWS resources and Amazon Connect instance are hosted, and have a stable connection to the public WAN\.

## Rerouting Audio<a name="reroute-audio"></a>

When rerouting audio to an existing device, consider the location of the device in relation to your Amazon Connect Region\. This is so you can account for potential additional latency\. If you reroute your audio, whenever there is a call intended for the agent, an outbound call is placed to the configured device\. When the agent answers the device, that agent is connected with the caller\. If the agent does not answer their device, they are moved into a missed contact state until they or a supervisor changes their state back to available\.

## Using AWS Direct Connect<a name="using-directconnect"></a>

Contact Control Panel \(CCP\) network connectivity issues are most often rooted in your route to AWS via private WAN/LAN, ISP, or both\. While AWS Direct Connect does not solve issues specific to private LAN/WAN traversal to your edge router, it can help solve for latency and connectivity issues between your edge router and AWS resources\. AWS Direct Connect provides a durable, consistent connection rather than relying on your ISP to dynamically route requests to AWS resources\. It also allows you to configure your edge router to redirect AWS traffic across dedicated fiber rather than traversing the public WAN\.