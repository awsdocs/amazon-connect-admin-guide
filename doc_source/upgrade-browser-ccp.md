# My CCP URL ends with /ccp\#<a name="upgrade-browser-ccp"></a>

Upgrading to the latest CCP is easy\. If you want, you can try out the latest CCP and then at a later date make the switch\. Here's what you do:

1. **Try it out**: Change the URL in your browser from **/ccp\#** to **/ccp\-v2**\. The latest CCP appears automatically\. If you want, change it back to /ccp\# to return to the earlier CCP\. 

1. **Upgrade**: Change the URL in your browser from **/ccp\#** to **/ccp\-v2**\. Bookmark the URL\. 

1. If you access the CCP through the Amazon Connect console by choosing the phone icon on the top right of a page, you will be re\-directed according to the automatic upgrade date sent by email\. Please reach out to your Amazon Solution Architect if your request is more urgent\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-phone-icon.png)

1. After the upgrade happens, if you use the /ccp\# URL, it resolves to **/ccp\-v2**\.

## Verify your network settings<a name="upgrade-verify-network-settings"></a>

We highly recommend setting up your network to use [Option 1 \(recommended\): Replace Amazon EC2 and CloudFront IP range requirements with a domain allow list](ccp-networking.md#option1)\. 

Using this option helps Amazon Connect Support to quickly troubleshoot any issues you have\. Specifically, using **\*\.execute\-api\.\{region\}\.amazonaws\.com** passes more metrics to our Support team to help with troubleshooting\. 

## Update your SAML URL to ccp\-v2<a name="update-saml-url"></a>

If you use SAML 2\.0 as your identity management system, be sure to update the destination in your relay state URL to **ccp\-v2**\. 

Change `destination=/connect/ccp` to `destination=/connect/ccp-v2`\.

For more information, see [Use a destination in your relay state URL](configure-saml.md#destination-relay)

## Compare the earlier and latest CCP<a name="ui-comparison"></a>

The images in this section show you how the latest CCP differs from the earlier CCP for common tasks that agents perform\. The images show both CCP versions in their default state\. 

**Tip**  
The chat tab appears on an agent's CCP only if their routing profile includes chat\.

### Set status, use chat, access quick connects and number pad<a name="ui-comparison-set-status"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-status-available.png)

1. Agents use a dropdown to set their status\.

1. If you have enabled chat for the agent’s routing profile, the chat tab appears\.

1. Choose the **Quick connects** button to type and call a phone number, or select a quick connect\.

1. Choose the **Number pad** button to type and call a phone number\. This is useful when the phone number has letters\.

### Receive a call<a name="ui-comparison-receive-call"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-receive-call-earlier-ccp.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-receive-call-latest-ccp.png)

### Miss a call<a name="ui-comparison-missed-call"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-missed-call.png)

### Make a call: When to use Quick connects<a name="ui-comparison-make-call"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-make-call.png)
+ Use the **Quick connects** button to type a number or select a quick connect\.

### Make a call: When to use Number pad<a name="ui-comparison-make-call-use-number-pad"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-make-call2.png)
+ Choose the **Number pad** button to type and call a number\. This is useful for corporate numbers with letters \(for example, 1\-800\-EXAMPLE\)\. 

### Make an outbound call<a name="ui-comparison-make-outbound-call"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-connected-outbound-call-earlier.png)

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-connected-outbound-call-latest.png)

### Agent ends a call before being connected to the other party<a name="ui-comparison-agent-ends-call-before-connecting"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-end-outbound-call-before-connecting.png)

1. If an agent ends a call before being connected, they are then available for a new contact to be routed to them automatically\.

1. If an agent ends a call before being connected, they are prompted to choose **Clear contact**\.

### Make another call while connected on a call<a name="ui-comparison-another-call"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-another-call.png)

1. You can see the call that you are on while typing another number or selecting a quick connect\.

1. After choosing **Quick connects**, you can choose the **Number pad** button\. Then on the **Number pad** page, you can enter a number\.

### Enter DTMF input while connected on a call<a name="ui-comparison-dtmf"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-dtmf.png)
+ While on a call, only use **Number pad** to enter DTMF input\. 

### Conference call scenario 1: Leaving a call when one party is on hold and the other is connected<a name="ui-comparison-conference-call1"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-conference-call.png)

1. Choose **Leave call** to leave the call\. This automatically takes the first party off hold and connects them to the second party\.

1. If instead you want to end the call, choose the **x** next to each party's number\. This disconnects each party\.

### Conference call scenario 2: Leaving a call when the other parties are joined<a name="ui-comparison-conference-call2"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-leave-call-keep-others-joined.png)

1. Choose **Leave call** to leave the call\. The other two parties stay joined\. 

1. If instead you want to end the call, choose the **x** next to each party's number\. This disconnects each party\.

### Conference call scenario 3: Leaving a call when the other parties are on hold<a name="ui-comparison-conference-call3"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-on-hold.png)

1. Choose **Leave call** to leave the call\. The other two parties are automatically taken off hold and connected\. 

1. If instead you want to end the call, choose the **x** next to each party's number\. This disconnects each party\. 

### Receive a queued callback<a name="ui-comparison-receive-queued-callback"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-receive-callback.png)

### Miss a queued callback<a name="ui-comparison-miss-queued-callback"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-miss-callback.png)

### Finish After contact work \(ACW\)<a name="ui-comparison-acw"></a>

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/upgradeccp-acw.png)
+ During After contact work \(ACW\), agents can finish follow\-up work, and then choose **Clear contact**\.