# Search conversations<a name="search-conversations"></a>


|  | 
| --- |
| Contact Lens for Amazon Connect is in preview release and is subject to change\. | 

After a call ends and the agent completes After Contact Work \(ACW\), Contact Lens analyzes and transcribes the recording of the customer\-agent conversation\.

You can search the analyzed and transcribed recordings based on: 
+ Speaker\.
+ Keywords\.
+ Sentiment score\.
+ Non\-talk time\.

Each of these criteria is described in the following sections\.

## Search for keywords<a name="keyword-search"></a>

For search, Contact Lens uses the `standard` analyzer in Amazon Elasticsearch Service\. This analyzer is case\-insensitive\. For example, if you enter *thank you for your business 2 CANCELLED Flights*, the search looks for:

 \[thank, you, for, your, business, 2, cancelled, flights\]

If you enter *"thank you for your business", two, "CANCELLED Flights"*, the search looks for:

 \[thank you for your business, two, cancelled flights\]

**To search conversations for keywords**

1. In Amazon Connect, choose **Metrics and quality**, **Contact search**\.

1. In the **Filter** section, specify the time period that you want to search\. Include other information to narrow your search\. For instructions, see [Contact search](contact-search.md)\.
**Tip**  
When searching by date, you can search up to 14 days at a time\. 

1. In the **Conversation** section, enter the words to search, separated by commas\. If you're entering a phrase, surround it with quotation marks\.

   You can enter up to 128 characters\.
   + Choose **Match any** to return contacts that have any of the words present in the transcripts\.

     For example, the following query means match \(hello OR cancellation OR "example airline"\)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/match-any.png)
   + Choose **Match all** to return contacts that have all of the words present in the transcripts\. 

     For example, the following query means match \("thank you for your business" AND cancellation AND "example airline"\)\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/match-all.png)

## Search for sentiment score<a name="sentiment-search"></a>

With Contact Lens, you can search conversations for sentiment scores on a scale of \-5 \(most negative\) to \+5 \(most positive\)\. This enables you to identify patterns and factors for why calls go well or poorly\.

For example, suppose you want to identify and investigate all the calls where the customer sentiment ended negatively\. You might search for all calls where the sentiment score is **<=** \(less than or equal to\) \-4\. 

**To search for sentiment scores**

1. On the **Contact search** page, specify whether you want the score words or phrases spoken by the customer or agent\.

1. In **Type of score analysis**, specify whether you want to return scores that are:
   + **>=** greater than or equal to \.\.\.
   + **<=** less than or equal to \.\.\.

   \.\.\.the specified sentiment score\.

## Search for non\-talk time<a name="nontalk-time-search"></a>

To help you identify which calls to investigate, you can search for non\-talk time\. For example, you might want to find all calls where the non\-talk time is greater than 20%, and then investigate them\.

Non\-talk time includes hold time and any silence where both participants aren't talking for longer than three seconds\. This duration can't be customized\.

Use the drop\-down arrow to specify whether to search conversations for the duration or percentage of non\-talk time\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/non-talk-time.png)