# DisconnectParticipant<a name="participant-actions-disconnectparticipant"></a>

Disconnects the participant from the contact and stops this flow from running\. 

## Parameter object<a name="disconnectparticipant-parameter"></a>

```
{
                
}
```

## Results and conditions<a name="disconnectparticipant-results"></a>

None\. Conditions are not supported\.

## Errors<a name="disconnectparticipant-errors"></a>

None\.

## Restrictions<a name="disconnectparticipant-restrictions"></a>

None\. This action can be used everywhere\. If there is no participant on the contact, this functions as an EndFlowExecution action, and halts the flow from running\. 

## Corresponding block in the UI<a name="disconnectparticipant-ui"></a>

[Disconnect / hang up](disconnect-hang-up.md)