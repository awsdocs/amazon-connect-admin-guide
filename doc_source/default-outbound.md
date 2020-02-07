# Default Outbound: "This call is not being recorded"<a name="default-outbound"></a>

This contact flow is an outbound whisper that manages what the customer experiences as part of an outbound call, before being connected with an agent\. 

1. It starts with an optional **Set recording behavior** block\. Then a prompt plays the following message: 

   *This call is not being recorded\.*

1. The flow ends\.

1. The customer remains in the system \(on the call\) after the flows ends\. 