# Automatically associate the Contact Record with one profile found using the \_phone key<a name="auto-associate-profile-using-phone-profile-key"></a>

You can automatically associate the Contact Record with one profile found using the `_phone` key\.

**Example**

In the domain, the following profile is created by the `CreateProfile` API:

```
            {
                "FirstName": "John",
                "LastName": "Doe",
                "PhoneNumber": "+11234567890"
            }
```

When a call is received from the `PhoneNumber` \+11234567890 using the default CTR template, the Contact Record will not be automatically associated with the above profile unless an agent has already manually associated the Contact Record with the same caller to the above profile\. If the Contact Record was not associated manually or automatically, Customer Profiles will create an inferred profile with the information from the Contact Record\.

To automatically associate the above profile with contact records without manual agent intervention, you can use the CTR\-NoInferred template\. When a call is received from the `PhoneNumber` \+11234567890 using the CTR\-NoInferred template, the Contact Record will automatically associate with the above profile using the `_phone` profile key\.

There are two scenarios in which Customer Profiles will *not* be able to automatically associate Contact Records to a profile:
+ If more than one profile is found using the `_phone` profile key, Customer Profiles cannot associate the Contact Record to a unique profile and the request will be rejected\.
+ If no profile is found for the `_phone` profile key, Customer Profiles will create an inferred profile\.

To use the CTR\-NoInferred template to replace the default CTR template, run the following command on the CLI:

`aws customer-profiles put-profile-object-type --domain-name {domain} --object-type-name CTR --description "No inferred contact record profiles" --template-id CTR-NoInferred`

To revert to the default behavior, run the following command on the CLI:

`aws customer-profiles put-profile-object-type --domain-name {domain} --object-type-name CTR --description "No inferred contact record profiles" --template-id CTR`