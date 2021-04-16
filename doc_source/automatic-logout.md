# Log out agents automatically when they close their CCP<a name="automatic-logout"></a>

When using the default Amazon Connect CCP, closing the CCP window doesn't change an agent's status from **Available** to **Offline**\. An agent must change their status manually to **Offline** and then log out\.

To change this behavior, you must create a custom CCP\.

Use the [Amazon Connect Streams API](https://github.com/amazon-connect/amazon-connect-streams) and the [Agent API](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#agent-api) to create a custom CCP for your contact center\. For an example custom CCP setup, see [Perform an external screen pop with Amazon Connect](http://aws.amazon.com/blogs/contact-center/perform-an-external-screen-pop-with-amazon-connect/)\. 

Use the following steps to update your CCP so it switches agents to **Offline**  and logs out agents automatically when they close the CCP window\.

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

1. Call [agent\.setState\(\)](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#agentsetstate--agentsetstatus) in the onbeforeunload event handler to change the agent state\.

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

If an API call fails to execute the first time and a contact takes the error branch of your contact flow, there's a chance that an agent's state won't change as expected\. Be sure to include logic to account for this possibility\. For example, you could delay the page unload while the API call is tried again\. Or, you could pop a "Call failed" warning message in a modal dialog before the page unload\.