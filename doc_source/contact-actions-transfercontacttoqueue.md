# TransferContactToQueue<a name="contact-actions-transfercontacttoqueue"></a>

This action places a contact that is not already in a queue into the contact's TargetQueue\. If the contact has already been put into a queue \(meaning that it is currently being routed to an agent, being joined to an agent, or is connected to an agent\), the action fails\. 

## Parameter object<a name="transfercontacttoqueue-parameter"></a>

No parameters are expected\.

## Results and conditions<a name="transfercontacttoqueue-results"></a>

None\.

## Errors<a name="transfercontacttoqueue-errors"></a>
+ QueueAtCapacity \- if the destination queue is at capacity and the contact cannot be queued within it\.
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="transfercontacttoqueue-restrictions"></a>

This action is supported in inbound contact flows and transfer flows\. It is not supported in whisper flows, customer queue flows, or hold flows\. 

## Corresponding block in the UI<a name="transfercontacttoqueue-ui"></a>

[Transfer to queue](transfer-to-queue.md)