# CCPv1: Log out agents automatically when they close their CCP<a name="automatic-logout"></a>

**Important**  
This topic only applies to customers who use CCPv1\. The URL for CCPv1 ends with **/ccp\#**\.

When using the default Amazon Connect CCPv1, closing the CCP window or logging out doesn't automatically change an agent's status from **Available** to **Offline**\. An agent must change their status manually to **Offline** and then log out\.

To change this behavior, you can do one of the following:
+ Use CCPv2\. When agents log out, their status is automatically switched to **Offline**\. However, note that CCPv2 doesn't automatically switch agents to **Offline** if they only close the window\. For instructions on upgrading to CCPv2, see [My CCP URL ends with /ccp\#](upgrade-browser-ccp.md)\.
+ Use the [CreateAgentStatus](https://docs.aws.amazon.com/connect/latest/APIReference/API_CreateAgentStatus.html) API: You can change the state of the agent to Offline\. 
+ Create a custom CCP\. See [Amazon Connect Streams API](https://github.com/amazon-connect/amazon-connect-streams) and the [Agent API](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#agent-api)
+ Use the following steps in this topic to update your CCP so it switches agents to **Offline**  and logs out agents automatically when they close the CCP window\.

## Step 1: Set up the Streams API<a name="automatic-logout-for-agents-step1"></a>

For instructions, see the [Amazon Connect Streams Documentation](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md)\. 

## Step 2: Update your application code to change the agent state<a name="automatic-logout-for-agents-step2"></a>

Integrate the following Streams API calls into your web application:

1. Use [connect\.agent\(\)](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#connectagent) to subscribe to agent events and retrieve agent objects\.

   ```
   let mAgent;
   
   connect.agent(function(agent) {
     mAgent = agent;
   });
   ```

1. Call [agent\.setState\(\)](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#agentsetstate--agentsetstatus) in the onbeforeunload event handler to change the agent state\. The agent is marked Offline after executing the `beforeunload` function\.

   Using the `beforeunload` hook is the best option, but note that it doesn't work consistently\. 

   ```
   window.addEventListener("beforeunload", function(event) {
       if (mAgent != null) {
           let states = mAgent.getAgentStates();
           // "states" is an array of changeable states. You can filter the desired state to change by name.
           let offlineState = states.filter(state => state.name === "Offline")[0];
                         
           // Change agent state
           mAgent.setState(offlineState, {
           success: function() {
               console.log("SetState succeeded");
           },
           failure: function() {
           console.log("SetState failed");
           }
       });
     }
   });
   ```

## Step 3: Design for errors<a name="automatic-logout-for-agents-step3"></a>

If an API call fails to execute the first time and a contact takes the error branch of your flow, there's a chance that an agent's state won't change as expected\. Be sure to include logic to account for this possibility\. For example, you could delay the page unload while the API call is tried again\. Or, you could pop a "Call failed" warning message in a modal dialog before the page unload\.