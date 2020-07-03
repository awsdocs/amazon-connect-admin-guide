# Resume a contact flow after transfer<a name="contact-flow-resume"></a>

Let's say you need to transfer a contact to an external department that's not using Amazon Connect\. For example, maybe you need to transfer the caller to a shipping provider to check the status of their delivery\. After the contact is disconnected from the external number, you want them to be returned to your agent, for example, when the delivery company couldn't resolve their issue\. 
+ For advanced automation, send tracking information as DTMF digits when the call is transferred, so that the shipment information is retrieved with the transferred call before the customer is connected\.

**To set up a contact flow for this scenario**

1. Add a **Transfer to phone number** block to your contact flow\.

1. In the **Transfer to phone number** block, enter the following settings:
   + **Transfer to**
     + **Phone number**—Sets the phone number to transfer the call to\.
     + **Use attribute**—Specify a contact attribute to set the phone number to transfer the call to\.
   + **Set timeout**
     + **Timeout \(in seconds\)**—The number of seconds to wait for the recipient to answer the transferred call\.
   + **Use attribute**—Specify a contact attribute to use to set the **Timeout** duration\.
   + **Resume contact flow after disconnect**—When you select this option, after the call is transferred, the caller is returned to the contact flow when the call with the third party ends\. Additional branches for **Success**, **Call failed**, and **Timeout** are added to the block when you select this option so that you can appropriately route contacts when there is an issue with the transfer\.
   + **Optional parameters**
     + **Send DTMF**—Select **Send DTMF** to include up to 50 Dual\-Tone Multi\-frequency \(DTMF\) characters with the transferred call\. You can enter the characters to include, or use an attribute\. Use the DTMF characters to navigate an automated IVR system that answers the call\.
     + **Caller ID number**—Specify the caller ID number used for transferred call\. You can select a number from your instance, or use an attribute to set the number\.
     + **Caller ID name**—Specify the caller ID name used for the transferred call\. You can enter a name, or use an attribute to set the name\.

       In some cases, the caller ID information is provided by the carrier of the party you are calling\. The information may not be up\-to\-date with that carrier, or the number may get passed differently between systems because of hardware or configuration differences\. If that is the case, the person you call may not see the phone number, or may see the name of a previously registered owner of the number, instead of the name you specify in the block\.

1. Connect **Transfer to phone number** to the rest of your contact flow\.

When the block executes: 

1. The call is transferred to the external number\.

1. Optionally, when the conversation with the external party ends, the contact is returned to the contact flow\.

1. The contact then follows the **Success** branch from the block to continue the flow\.

1. If the call is not successfully transferred, one of the other branches is followed: **Call failed**, **Timeout**, or **Error**, depending on the reason the caller did not return to the flow\.