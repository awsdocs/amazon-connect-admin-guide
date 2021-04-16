# UpdateContactAttributes<a name="contact-actions-updatecontactattributes"></a>

Behaving the same as the public API, this sets a collection of contact attributes\. With this type of operation, either all attributes are set or none are set\. 

## Parameter object<a name="updatecontactattributes-parameter"></a>

```
{
    "Attributes": { an Object that holds the attributes to be set. 
        "Key": "Value" Both the key and value may be defined statically or dynamically.
    }
}
```

## Results and conditions<a name="updatecontactattributes-results"></a>

None\.

## Errors<a name="updatecontactattributes-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Restrictions<a name="updatecontactattributes-restrictions"></a>

None\. This can be used in any type of flow and any channel\. 

## Corresponding block in the UI<a name="updatecontactattributes-ui"></a>

[Set contact attributes](set-contact-attributes.md)