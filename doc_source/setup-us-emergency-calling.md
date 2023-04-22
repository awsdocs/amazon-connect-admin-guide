# Set up US emergency calling in Amazon Connect<a name="setup-us-emergency-calling"></a>

By default 911 is enabled for all users in the following North America Regions: US East \(N\. Virginia\), US West \(Oregon\), and AWS GovCloud \(US\-West\)\. If an agent calls 911, the call is routed through to emergency services\.

**What is Enhanced 911 \(E911\)?** E911 enables location information to be sent to 911 dispatch when a 911 call is placed\.

There are two steps to set up E911:
+ [Get and store an agent's validated physical address](get-and-store-agent-address-e911.md) 
+ [Retrieve an agent's address when they call 911](retrieve-agent-address-e911.md) 

## Place 911 calls from your Test Environment<a name="connect-test-e911"></a>

**Important**  
Calling 911 for a non\-emergency situation carries a penalty of $100 per occurrence\. To help you avoid penalties, we have set up 933 so you can test this capability\. Calls placed from an Amazon Connect Contact Control Panel \(CCP\) to 933 have an audio playback message confirming:  
The number the call originated from\.
The physical address that was sent along with the call\. 

For more information about calling 911, see this [FAQ](https://www.911.gov/calling-911/frequently-asked-questions/) about the national 911 program\. 