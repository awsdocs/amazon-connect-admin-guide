# Optimize your reputation for outbound calling<a name="optimize-outbound-calling"></a>

In the contact center industry one of the most difficult tasks is understanding why customers don't answer calls when you dial out\. Is the customer deliberately not answering, or are they busy on a work call or answering the door? For contact centers it's impossible to know but there are things you can do about it\.

This topic provides recommended steps you can take to improve your call answer rates for outbound calling\. 

## Step 1: Know your customer's preferred contact method<a name="know-customer-preferred-contact-method"></a>

One of the biggest mistakes that contact centers make is not knowing whether the customer wants to be contacted by telephone call\. When the customer engaged with you, did you check whether they want to be reached by phone, e\-mail, or text?

Businesses with multi\-channel engagement outperform 70% on average compared to business without multi\-channel engagement\. 

## Step 2: Brand your calls<a name="brand-your-calls"></a>

By using call branding solutions, you can provide enhanced call displays that include your business name, logos, reason for the call, and your service\. Branding your calls increases the call answer it by 30%\. 

Amazon Connect partners with solution providers for branding the calls\. To locate partners who provide this service, search the [Amazon Connect Partners](http://aws.amazon.com/connect/partners/) site for **branded call display**\. 

## Step 3: Select caller IDs that mean something to your customer<a name="meaningful-callerid"></a>

Not every contact center is the same\. What works for some might not work for others\. But there are correlations in how successful outbound campaigns are based on your caller ID\. Following are a few suggestions to try creating meaningful caller IDs: 
+ **Area localization**\. Use a caller ID in the same area as the prospect\.
+ **City localization**\. Use a caller ID in the same city as the prospect\.
+ **Recognizable golden toll free number** such as 0800 123 0000\.
+ **Mobile numbers**\. Where countries permit this, it may be possible to use a virtual mobile number to dial out from a contact center\. For a list of countries where Amazon Connect supports mobile numbers, see [Region requirements for ordering and porting phone numbers](phone-number-requirements.md)\.

## Step 4: Make sure your campaign is calling valid numbers<a name="call-valid-numbers"></a>

Many businesses don't have a process to ensure that customer details are up to date\. With people being more mobile than ever, it's essential for businesses to keep updated contact information\. If customers are not answering your calls, we recommend using Amazon Pinpoint to [validate your phone numbers](https://docs.aws.amazon.com/pinpoint/latest/developerguide/validate-phone-numbers.html)\. It may be the customer is no longer at the phone number you are calling\. 

## Step 5: Make outbound calls at optimal times<a name="optimal-times"></a>

Another strategy for outbound call campaigns is making sure that calls are placed at the best times\. It is critical to never harass your customers or prospects—no one wants to be contacted multiple times by the same company\. Generally speaking, it is never a good idea to call before 10:00AM or after 5:00PM as people are at their busiest or need their quiet time\. Customers should be called when it's a good for them, depending on their profile\. This may mean that one customer should be called around noon, while another is more accessible in the afternoon\. 

In addition, there are regulations such as TCPA \(in the US\) and OFCOM \(in the UK\) that provide guidance on when not to call end customers\. We strongly recommend that you abide by such regulations\.

## Step 6: Monitor the reputation of your caller IDs<a name="monitor-reputation"></a>

We recommend monitoring the reputation of your caller ID through a service like [Free Caller Registry](https://www.freecallerregistry.com/)\. 

Even with the most legitimate outbound call campaigns, if you make enough calls, there will be people who will flag your caller ID as spam\. This can manifest in two ways:

1. **Automatic blocking**\. Block lists are implemented on a vendor\-by\-vendor basis\. For example, when a certain threshold of reports is reached with application providers such as [Hiya\.com](https://www.hiya.com/) on Samsung devices, up to 20% of your prospects will become instantly unreachable\.

1. **Complaints**\. There are numerous websites where people complain about calls from specific caller IDs\. A number of your prospects will search your caller ID online when you call them\. If it has a bad reputation, they will be less likely to answer\.

The fastest way to recover from a flagged caller ID is to switch to a new phone number\. See the next step\.

## Step 7: Use multiple numbers as a callerID<a name="use-multiple-numbers"></a>

Today, outbound contact centers typically embrace an intelligent, more efficient manner of dialing\.

For example, one method is to use multiple phone numbers when placing outbound calls\. Customers are more likely to answer a call if they feel that they are not being called repeatedly by the same number\. In fact, using the same phone number repeatedly is a sure way to annoy customers and prospects who may feel they are being contacted too often\.

## Step 8: Engage with App Vendors<a name="engage-inapp-vendors"></a>

One of the most difficult issues with the industry as it currently stands is that a large number of vendors provide in\-app services to block calls\. If one of these in\-app services marks your number as spam then you have to pay the premium fees to remove your number from their spam list\. 

Some of the third party vendors are joining in partnership to increase the call answer rate\. 

## Step 9: Add messaging to your outreach strategy to let customers know who you are<a name="add-messaging"></a>

It's inevitable that you'll end up with a list of unanswered calls that you weren't able to connect\. There are a variety of creative ways to use SMS with prospects\. Here are some ideas to increase answer rates with your prospects\.

1. Send an SMS before calling, letting them know who you are and when you will be calling, optionally allowing them to reschedule to a more convenient time\.

1. If the prospect doesn't answer, send an SMS to allow them to reschedule the call or request a call back\.

1. Re\-engage with prospects with promotional offers or discounts that resonates with your prospects\.

## Step 10: Validate your outbound calling strategy<a name="validate-calling-strategy"></a>

By making data\-driven decisions and continuously iterating, you'll have the best chance to deliver real business value\. You should treat each change that you make to your outbound calling strategy as an experiment, and ensure you have the ability to measure and compare the effectiveness of the changes you are making\. 

One of the best things with Amazon Connect is the service is readily available to experiment\. You can establish a baseline and then compare any changes to help you to assess how you can succeed\. 