# UpdateContactCallbackNumber<a name="contact-actions-updatecontactcallbacknumber"></a>

Updates the contact callback number, which is the number used by the CreateCallbackContact action\. This value defaults to the customer participant caller ID if this action is never used\. 

## Parameter object<a name="updatecontactcallbacknumber-parameter"></a>

```
{
    "CallbackNumber": The callback number to set. Must be a single, valid JSONPath reference, and cannot be set statically. 
}
```

## Results and conditions<a name="updatecontactcallbacknumber-results"></a>

None\.

## Errors<a name="updatecontactcallbacknumber-errors"></a>
+ InvalidCallbackNumber \- The callback number specified was not a valid \(e\.164\) phone number\.
+ CallbackNumberNotDialable \- The callback number specified is not dialable by the instance\.

## Restrictions<a name="updatecontactcallbacknumber-restrictions"></a>

This is supported only in contact flows, transfer flows, and customer queue flows\. This is not supported in whispers or hold flows\. 

## Corresponding block in the UI<a name="updatecontactcallbacknumber-ui"></a>

[Set callback number](set-callback-number.md)