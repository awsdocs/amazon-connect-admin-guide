# Accept incoming contacts with Customer Profiles<a name="select-customer-profile"></a>

When a call or chat is connected to your Contact Control Panel \(CCP\), Amazon Connect, in the same browser window, automatically displays customer profiles that may match the incoming phone number\. 

Before agents can access customer profiles, the Amazon Connect administrator must enable the Customer Profiles feature, grant agents the appropriate permissions, and integrate Customer Profiles into your agent application\. For more information, see [Enable Customer Profiles for your instance](enable-customer-profiles.md)\.

## Example 1: Auto\-populate the customer profile<a name="example1-select-customer-profile"></a>

As soon as Amazon Connect matches the phone number \(voice\) or email address \(chat\) with an existing customer profile, it automatically displays the profile even though you may not have accepted the contact yet\.

The following image shows what your Contact Control Panel \(CCP\) may look like when there's an incoming chat\. A customer profile has been found that matches the customer, and Amazon Connect is loading the data\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-incoming-chat-example1.png)

This next example shows what it might look like after you've accepted and joined the chat, and Amazon Connect displays the customer's profile\. In this case, Amazon Connect found the customer's profile based on their email address\. If this were a voice call, by default Amazon Connect would match the customer's profile based on their phone number\. Your IT department can [customize](auto-pop-customer-profile.md) this behavior to search for the profile based on other information about the contact\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-choose-profile-example1.png)
+ Choose **Associate** to associate the contact record of the current contact with the customer profile, and then choose **Confirm**\.   
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-choose-profile-example1a.png)
+ If you choose **Associate** by mistake, you can continue to browse other customer profiles, and associate the contact with a different customer profile\. Or, if you have been [assigned Create permission](assign-security-profile-customer-profile.md), you can create a new profile\. 

  You can associate a contact with customer profile multiple times during an interaction, including during After Contact Work \(ACW\) time\. Only the most recent association remains, before you clear the contact\.

## Example 2: Accept incoming contact, no customer profile found<a name="example2-select-customer-profile"></a>

If no results are returned when a call or chat comes in, do the following: 

1. Search for the customer's profile using their email address, name, or account number\. An *account number* is a unique identifier for the customer in your business, such as a member number or a customer relationship number\. 

1. If no customer profile is found, [create a new profile](create-new-customer-profile.md) for the contact\. The only required information is first name\.

In the following image, the agent searched for **John Doe**\. No matches were found so they chose **Create profile**\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-no-profiles-found.png)

## Example 3: Accept incoming contact, multiple customer profiles found<a name="example3-select-customer-profile"></a>

In some cases, multiple profiles may be returned for the same call or chat\. Use the summary information to verify the customer's identity\. For example, ask the customer to verify their email address or account number, and then associate the contact with the right customer profile\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-choose-profile-example3.png)

## Example 4: Search when not on contact<a name="example4-select-customer-profile"></a>

When there are no incoming contacts, you can search for customer profiles using phone number, name, email address, or account number\. For example, you might want to use this time to search for previous contacts, or completing a profile\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/customer-profiles-search-not-connected-example4.png)