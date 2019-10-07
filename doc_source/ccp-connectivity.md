# CCP Connectivity<a name="ccp-connectivity"></a>

When an agent logs in, the CCP attempts to connect to the Amazon EC2 signaling endpoints listed in the AWS ipranges\.json file, Amazon Connect for media, and CloudFront for web artifacts such as images\. When the agent logs out or the browser is closed, endpoints are reselected when the agent next logs in\. If a connection to Amazon EC2 or Amazon Connect fails, errors display on the CCP\. If a connection to CloudFront fails, web elements such as buttons and icons, or even the page itself fails to load correctly\.

**Outbound calls**
+ When an outbound call is placed, the event signal is sent to the Amazon EC2 endpoint, which then communicates with Amazon Connect to place the call\. Upon a successful dial attempt, the agent is bridged in, which anchors the call to the agent's Amazon Connect endpoint\. Any external transfers or conferences also uses the anchor until the call is disconnected\. Anchoring can help reduce PSTN latency\.

**Inbound calls**
+ When an inbound call is received, the call is anchored to an Amazon Connect endpoint\. Any external transfers or conferences also use this anchor until the call is disconnected\.
+ When an agent is available, the call is pushed through via a new Amazon EC2 connection to their browser and offered to the agent\.
+ When the agent accepts the call and either the external device has been answered or the CCP determines it can receive a call, a connection to Amazon Connect is established for call media to the agent\.

**Transferred calls**
+ When a call is transferred, the transfer event that signals to place an outbound call to the specified transfer destination is sent to Amazon EC2, which then communicates with Amazon Connect to place the call\.
+ When the call is connected, the agent is bridged in, anchoring the call to the agent's existing Amazon Connect endpoint\. Any external transfers or conferences also use this anchor until the call is disconnected\.
+ If the agent hangs up after the call is bridged, the agent's connection to the call is terminated, but Amazon Connect hangs on to the call at the Amazon Connect anchor point until there is a far side disconnect\. When the call is disconnected, CTRs and associated recordings are generated and made available for the call\.

**Missed calls**
+ If the call is waiting on an agent, customer queue flow logic is used until an agent is available and the call has been successfully routed to that agent\.
+ If the agent does not accept the call, the agent moves into a Missed Call state and is unable to take calls until the agent, or a call center manager, changes their status to Available again\. The caller does not hear ringing while the call is waiting for the agent, and continues to hold until connected with an agent as defined in the customer queue flow logic\. 

**Panic logout**
+ If the browser window where the CCP is running is closed, the call remains connected, but opening the browser and logging back in will not allow you to re\-establish the media connection\. You are still able to transfer or end the call, but no audio path is established between the agent and caller\.