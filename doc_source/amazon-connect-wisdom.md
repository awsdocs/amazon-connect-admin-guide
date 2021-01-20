# Amazon Connect Wisdom: Get the content you need<a name="amazon-connect-wisdom"></a>


|  | 
| --- |
| The Amazon Connect Wisdom feature is in preview release for Amazon Connect and is subject to change\. | 

With Amazon Connect Wisdom, agents can search and find content across multiple repositories, such as frequently asked questions \(FAQs\), wikis, articles, and step\-by\-step instructions for handling different customer issues\. They can type questions or phrases in a search box \(such as, "how long after purchase can handbags be exchanged?"\) without having to guess which keywords will work\.

If your organization uses real\-time analytics from Contact Lens for Amazon Connect to automatically detect customer issues during calls, then Amazon Connect Wisdom can proactively recommend information to help resolve the issue\. For example, Contact Lens can detect phrases such as "product broke during shipping" and then display text snippets, FAQs, and instructions for exchanging damaged products\.

The following image shows an agent's Contact Control Panel \(CCP\), and an example of how Amazon Connect Wisdom results may appear adjacent to it after an agent has searched for information\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wisdom-concepts-intro.png)

The following list refers to the designated areas in the preceding example:

1. Real\-time recommendations based on real\-time analytics

1. Search for words or phrases

1. Provide feedback on the helpfulness of the results

## Access Amazon Connect Wisdom with a new URL \(Preview\)<a name="new-url-wisdom"></a>

If you're using the CCP that is provided with Amazon Connect, after you enable Amazon Connect Wisdom, share the following URL with your agents so they can access it:

**Note**  
This link only works if you're signed up for the Amazon Connect Wisdom preview:  
**https://*instance name*\.awsapps\.com/connect/agent\-app/**

**Note**  
IT administrators: In the future, the access URL is going to change\. For the release schedule and technical details, see [Upcoming change: Domain for new Amazon Connect instances is "my\.connect\.aws"New domain for access URL](amazon-connect-release-notes.md#new-domain)\. 

By using the new URL, your agents can view the CCP and Amazon Connect Wisdom in the same browser window\.

If CCP is embedded in your agent's application, see [Amazon Connect Streams](https://github.com/aws/amazon-connect-streams) for information about how to include Amazon Connect Wisdom\. 

For more information about the agent's experience using Amazon Connect Wisdom, see [Search for content using Amazon Connect Wisdom](search-for-answers.md)\.