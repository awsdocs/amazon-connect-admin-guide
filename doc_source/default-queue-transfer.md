# Default queue transfer: "Now transferring"<a name="default-queue-transfer"></a>

This contact flow manages what the agent experiences when they transfer a customer to another queue\.

It starts with a **Check hours of operation** block to check the hours of operation for the current queue\. The **In hours** option branches to the **Check staffing** block to determine whether agents are available, staffed, or online\. 

If it returns **True** \(agents are available\), the flow goes to the **Transfer to queue** block\. If it returns **False** \(no agents are available\), the flow plays a prompt and disconnects the call\.

For instructions about how to override and change a default contact flow, see [Change a default contact flow](change-default-contact-flow.md)\.