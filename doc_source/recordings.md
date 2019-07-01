# Work with Recordings<a name="recordings"></a>

Managers can listen to and download recordings of agent calls\. To set this up, you need to add the **Set call recording behavior** block to your contact flows, grant managers the appropriate permissions, and show them how to access the recordings in Amazon Connect\. 

**To set up call recording in your contact flows**

1. Log in to your Amazon Connect instance using an account that has permissions to edit contact flows\.

1. Choose **Routing**, **Contact flows**, and then open the contact flow that handles customer contacts you want to listen in on\. 

1. Before the call is connected to an agent, add a **Set call recording behavior** block to the contact flow\. In the block, choose **Agent and Customer**, and then choose **Save**\.
**Important**  
Make sure that the block has connections to the block before and after it in the contact flow\.

1. To enable manager listen\-in and recording for outbound calls, the contact flow in which you add **Set call recording behavior** must be in the flow selected as the outbound contact flow for the queue used for outbound calls\.

1. Choose **Save and Publish** to publish the updated contact flow\. Choose **Save and Publish** again to confirm that you want to overwrite the published version\.

**To assign the manager permissions to listen in to recordings of conversations**

1. Go to **Users**, **User management**, choose the manager, and then choose **Edit**\.

1. In the Security Profiles box, assign the manager to the **CallCenterManager** security profile\. This security profile also includes a setting that makes the icon to download recordings easily discoverable\. 

1. Also assign the manager to the **Agent** security profile so they can access the control contact panel\. 

1. Choose **Save**\. 

## Listen to or Download Recordings<a name="w13aac13c23c13"></a>

**To listen to or download recordings of agents talking to customers**

1. Log in to your Amazon Connect instance with a user account that is assigned the **CallCenterManager** security profile, or that is enabled for the **Manager monitor** permission\.

1. To choose the agent call you want to listen in to, in Amazon Connect choose **Metrics and quality**, **Contact search**\. 

1. Filter the list of contacts by date, agent login, phone number, or other criteria\. Choose **Search**\.

1. Calls that were recorded will have icons in the Recording column\. Click to listen to a recording, download, or delete it\. If you choose to download the file, it will be saved automatically to your Downloads folder\. 