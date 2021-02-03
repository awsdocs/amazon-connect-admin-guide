# UpdatePreviousContactParticipantState<a name="contact-actions-updatepreviouscontactparticipantstate"></a>

This action is primarily used to forceably prevent previous participants on the contact from observing the contact\. Common use cases are disconnecting the agent that initiates a transfer when they transfer a contact to a secure destination, or putting the agent on hold when transferring to a quick connect that securely gathers customer input such as credit card numbers\. 

## Parameter object<a name="updatepreviouscontactparticipantstate-parameter"></a>

```
{
    "PreviousContactParticipantState": One of ["AgentOnHold", "CustomerOnHold", "OffHold"], which are only supported for voice contacts. 
}
```

## Execution results and conditions<a name="updatepreviouscontactparticipantstate-results"></a>

None\.

## Errors<a name="updatepreviouscontactparticipantstate-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="updatepreviouscontactparticipantstate-restrictions"></a>

This action is supported only in contact flows and transfer flows\. 

## Corresponding block in the UI<a name="updatepreviouscontactparticipantstate-ui"></a>

[Hold customer or agent](hold-customer-agent.md) 