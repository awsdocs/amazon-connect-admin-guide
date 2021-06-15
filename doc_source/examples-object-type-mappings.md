# Examples of object type mappings<a name="examples-object-type-mappings"></a>

## An object type mapping that generates a profile<a name="profile-generating-example"></a>

The following example shows data that populates the standard profile\.

Following is the incoming object:

```
{
  "account": 1234,
  "email": "john@examplecorp.com",
  "address": {
     "address1": "Street",
     "zip": "Zip",
     "city": "City"
  },
  "firstName": "John",
  "lastName": "Doe"
}
```

The following code shows that incoming object mapping into a standard profile object and indexing `PersonalEmailAddress`, `fullName`, and `accountId`, which is a unique key\.

```
{
    "Fields": {
        "accountId": {
            "Source": "_source.account",
            "Target": "_profile.AccountNumber",
            "ContentType": "NUMBER"
        },
        "shippingAddress.address1": {
            "Source": "_source.address.address1",
            "Target": "_profile.ShippingAddress.Address1"
        },
        "shippingAddress.postalCode": {
            "Source": "_source.address.zip",
            "Target": "_profile.ShippingAddress.PostalCode"
        },
        "shippingAddress.city": {
            "Source": "_source.address.city",
            "Target": "_profile.ShippingAddress.City"
        },
        "personalEmailAddress": {
            "Source": "_source.email",
            "Target": "_profile.PersonalEmailAddress",
            "ContentType": "EMAIL_ADDRESS"
        },
        "fullName": {
            "Source": "{{_source.firstName}} {{_source.lastName}}"
        },
        "firstName": {
            "Source": "_source.firstName",
            "Target": "_profile.FirstName"
        },
        "lastName": {
            "Source": "_source.lastName",
            "Target": "_profile.LastName"
        }
    },
    "Keys": {
        "_email": [
            {
                "FieldNames": ["personalEmailAddress"]
            }
        ],
        "_fullName": [
            {
                "FieldNames": ["fullName"]
            }
        ],
        "_account": [
            {
                "StandardIdentifiers": ["PROFILE","UNIQUE"],
                "FieldNames": ["accountId"]
            }
        ]
    }
}
```

Note that `email` and `fullname` are indexed, but they aren't used to search for the profile\. The account is the unique key\. It is required to specify the object\. Any time an object with the same account ID is ingested it overwrites the previous object with the same account ID\.

Several fields are populated in the standard profile object \(see the fields that have `Target` defined\)\.

## An object type mapping that doesn't populate the standard profile<a name="ticket-issue-example"></a>

This example shows a more complicated use case\. It ingests data related to a profile but it doesn't necessarily populate the standard profile object\.

Following is the incoming object:

```
{
  "email": "john@examplecorp.com",
  "timestamp": "2010-01-01T12:34:56Z",
  "subject": "Whatever this is about",
  "body": "Body of ticket"
}
```

Following is one way of mapping this data:

```
{
    "Fields": {
        "email": {
            "Source": "_source.email",
            "ContentType": "EMAIL_ADDRESS"
        },
        "timestamp": {
            "Source": "_source.timestamp",
            "Target": "_profile.ShippingAddress.Address1"
        }
    },
    "Keys": {
        "_email": [
            {
                "StandardIdentifiers": ["PROFILE","LOOKUP_ONLY"],
                "FieldNames": ["email"]
            }
        ],
        "ticketEmail": [
            {
                "StandardIdentifiers": ["PROFILE","SECONDARY","NEW_ONLY"],
                "FieldNames": ["email"]
            }
        ],
        "uniqueTicket": [
            {
                "StandardIdentifiers": ["UNIQUE"],
                "FieldNames": ["email","timestamp"]
            }
        ]
    }
}
```

This example ingests the data and, at first lookup, it ingests the email address\. 
+ If the email address matches a single profile, it is used to attach the data to that specific profile\. The unique identifier for the ticket is comprised of the email and the timestamp since no other unique identifier exists\.
+ If no profile exists with the specified email, a new profile is created with the single field of `EmailAddress` filled in\. The ingested object is attached to this new **inferred profile**\. The two searchable keys that can find the profile are `_email` and `uniqueTicket`\.
+ If more than one profile exists with the specified email address, a new profile is created with the single field of `EmailAddress` filled in and the object is attached to this new profile\. This profile is created with the `ticketEmail` key defined, in addition to `_email` and `uniqueTicket`\. Any subsequent tickets from that email are assigned to this new **inferred profile**\. The reason for this is that the ` _email` key is referring to three profiles and is thus discarded, however the `ticketEmail` key only refers to a single profile \(the new inferred one\) and is still valid\.
+ In cases where a new **inferred profile** is created, the `EmailAddress` field is populated from the first object that created it\.