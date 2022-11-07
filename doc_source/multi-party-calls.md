# Multi\-party calls: Add additional participants to an ongoing call<a name="multi-party-calls"></a>

You can add up to **4** additional participants to an ongoing customer service call, for a total of **6** participants\. 

By using quick connects or your number pad, you can add other agents, supervisors, or external participants\.

For example, to help close a mortgage transaction, an agent at a financial services company can add a mortgage broker, the customer's spouse, a translator, and a supervisor to the call to help resolve any issues quickly\. 

For information about how multi\-party calls differs from the default three\-party calls, see [Comparison: Three\-party and multi\-party calls](amazon-connect-release-notes.md#comparison-multi-party)\.

## Important things to know<a name="important-things-multi-party-calls"></a>
+ This feature is only available in CCPv2 and custom CCP using Amazon Connect Streams\.js\.
  + **IT administrators**: 
    + Before enabling the multi\-party calls feature, if you are using Contact Lens or planning to do so in the future, see [Multi\-party calls and Contact Lens](enable-analytics.md#multiparty-calls-contactlens)\.
    + By default, there can be three participants on a call \(for example, two agents and a caller, or an agent, a caller, and an external party\)\. Before enabling multi\-party calling, see [Comparison: Three\-party and multi\-party calls](amazon-connect-release-notes.md#comparison-multi-party)\. To enable agents to connect up to six parties on a call, see [Update telephony options](update-instance-settings.md#update-telephony-options)\.
  + **Developers**: In custom CCPs, use the updated Amazon Connect Streams API to enable multi\-party calling, up to six parties\. See the [Amazon Connect Streams](https://github.com/amazon-connect/amazon-connect-streams/blob/master/Documentation.md#connectcoreinitccp) documentation on GitHub\. Before enabling multi\-party calling, see [Comparison: Three\-party and multi\-party calls](amazon-connect-release-notes.md#comparison-multi-party)\.
+ **AWS GovCloud \(US\-West\)**: You can't enable this feature using the console user interface\. Instead, use the [UpdateInstanceAttribute](https://docs.aws.amazon.com/connect/latest/APIReference/API_UpdateInstanceAttribute.html) API or contact AWS Support\.

## How to add participants to a multi\-party call<a name="add-participants-multi-party-calls"></a>

1. The following image shows the contact and you \(the agent\) on a call\. The customer always appears at the top\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-multiparty-two-people.png)

1. While you're connected to the contact, choose **Quick connects** to add another agent or the **Number pad** to make an external call\. The caller is put on hold while you do this\. 

1. When you add the third participant to the call, you can greet and talk to them before adding them to the call \(for example, tell them why you are adding them to the call\)\. 

   The following image shows what the CCP looks like when you add a third participant to the call\. The contact is on hold, and you're talking to the third party\. Choose **Join** to take all parties off hold\. Or, choose **Swap** to toggle between the parties on hold and the party you just called\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-multiparty-join-second-person.png)
**Note**  
Swap is only available when there are three parties on a call \(for example, you, the caller, and another agent or external party\)\. It is not available when there are more than three parties on the call\.

1. When there are multiple agents on the call \(for example, three agents and a caller\), all agents on the call can view all parties and have the option to put any participant or another agent on hold, mute, and disconnect participants from the call\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-multiparty-mute-hold-drop1.png)

1. Every time you add a new participant to the call, you are prompted to greet and talk to them before adding them to the call\. Choose **Join** to take all parties off hold\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-multiparty-join-third-person.png)

## How to manage participants<a name="manage-participants-multi-party-calls"></a>

Every agent on the call has access to the controls next to each participant's number to mute, hold, or disconnect individual participants\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-multiparty-overview.png)

You can transfer a multi\-party call to another agent, or disconnect yourself from the ongoing call\. 

Choose the **More** button to open the number pad and to create a task:

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/ccp-multiparty-more-options.png)

## When do multi\-party calls end?<a name="end-multi-party-calls"></a>

A multi\-party call stays up as long as the caller or the agent is on the call\. For example, add an external party to a call and then you disconnect\. The caller and external party continue the call\. 

If only third\-parties are left on the line, the contact is terminated\. However, as the agent you can choose to disconnect and allow only the caller and the third\-party participants to remain on the call\. 