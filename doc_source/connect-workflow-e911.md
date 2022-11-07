# Build E911 capabilities into your Amazon Connect contact center<a name="connect-workflow-e911"></a>

In addition to connecting a user with 911 emergency services, customers in the United States can build E911 capabilities to automatically provide the caller's address information to 911 dispatchers\. 

Following is an example E911 workflow for Amazon Connect: 

1. The client application obtains the location/physical address of the Amazon Connect user who may need to call 911\. For example, the client application might prompt the agent for their location address\. See [Best practice to capture the agent address](#bp-capture-agent-address)\.

1. Your workflow stores the physical address in a database\.

1. The agent \(or other Amazon Connect user\) uses their Amazon Connect Contact Control Panel \(CCP\) to call 911\.

1. Your workflow provisions an AWS Lambda function that retrieves the physical address and provides it to Amazon Connect to proceed with the 911 call\.

The following image shows this E911 workflow\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/e911-workflow.png)

## Best practice to capture the agent address<a name="bp-capture-agent-address"></a>

Since agents may be working from different locations \(for example, office building, home, or coffee shop\), the most recently validated address should be passed along with the emergency outbound call\. 

We recommend storing a validated address when first setting up an agent on Amazon Connect based on the agent’s usual location and then prompting the agent to update their address at the start of an agent's shift to help ensure that the emergency outbound call has the latest address\. 

Addresses should be checked against a database of valid street addresses \(Master Street Address Guide\)\.