# Investigate non\-talk time during calls<a name="non-talk-time"></a>

## What is non\-talk time?<a name="what-is-non-talk-time"></a>

Contact Lens for Amazon Connect also identifies the amount of *non\-talk time******* in a call\. Non\-talk time equals hold time, plus any silence where both participants aren't talking for more than 3 seconds\. This duration can't be customized\.

The following image shows the location of non\-talk time data on the **Contact details **page\.

![\[The contact details page, the talk time section, the non-talk time data.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-nontalk-time-overview.png)

## How to investigate non\-talk time<a name="how-to-investigate-non-talk-time"></a>

Non\-talk time can help you identify calls that have gone poorly\. This may be because:
+ The customer was asking a question that's new for your contact center\.
+ It's taking the agent a long time to do something but they are well\-trained\. This indicates there may be an issue with the tools the agent is using\. For example, the tools aren't responsive enough or aren't easy to use\.
+ The agent didn't have a ready answer, but they are fairly new\. This indicates they need more training\.

You can decide whether to focus on these contacts to improve your contact center\. For example, you can go to that section of the audio, and then look at the transcript to see what was going on\.

 In the following example, the non\-talk time occurred when the agent was searching for the caller's trip ID\. This could indicate there's an issue with the agent's tools\. Or if the agent is new, they need more training\.

![\[The contact audio recording and transcript, the location of non-talk time.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/contact-lens-non-talk-time-transcript.png)

For more information, see [Search for non\-talk time](search-conversations.md#nontalk-time-search)\.