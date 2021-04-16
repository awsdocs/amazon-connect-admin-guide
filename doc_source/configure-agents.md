# Configure agent settings: routing profile, phone type, and auto\-accept calls<a name="configure-agents"></a>

Before you configure your agent settings, here is some info to have on hand\. Of course, you can always change this information later\. 
+ What is their routing profile? They can only be assigned one\. 
+ Will they have the **Agent** security profile or a custom profile you created? 
+ Are they going to use a soft phone? If so, will they be connected to contacts automatically, or will they need to press the **Accept** button in their Contact Control Panel \(CCP\)?
+ Or, are they going to use a desk phone? If so, what is their number?
+ How many seconds do they have for After contact work \(ACW\)?
+ Are they going to be assigned to an agent hierarchy?

**Note**  
You can't configure how long an available agent has to connect with a contact before it's missed\. Agents have 20 seconds to accept or reject a contact\. If no action is taken, the current agent's status will be **Missed** and the contact is routed to the next available agent\.

**To configure agent settings**

1. In the navigation pane, go to **Users, User management**\.

1. Choose the user you want to configure, then choose **Edit**\.

1. Assign a [routing profile](routing-profiles.md) to them\. You can only assign one\.

1. Assign the **Agent** security profile, unless you've created custom security profiles\.

1. Under **Phone Type** choose whether the agent is using a desk phone or soft phone\. 
   + If you select desk phone, enter their phone number\.
**Important**  
Outbound telephony charges occur when using a desk phone to answer inbound calls\.
   + If you select soft phone, choose **Auto\-Accept Call** if you want agents to be connected to calls automatically\. This doesn't apply to chats\. 

1. In **After call work \(ACW\) timeout**, type how many seconds agents have for after contact work, such as entering notes about the contact\. 1 second is the minimum amount of time you can enter\.

   Enter **0** if you don't want to allocate a specific amount of ACW time\. It essentially means an indefinite amount of time\. When the conversation ends, ACW starts; the agent must choose **Close contact** to end ACW\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/acw-timeout.png)

1. Under **Agent Hierarchy** select any groups the agent should be part of\.