# UpdateCustomerProfile<a name="interactions-updatecustomerprofile"></a>

Update a customer profile that was previously created or retrieved in the flow\. Customer Profiles must be enabled for your Amazon Connect instance\.

See [UpdateProfile](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_UpdateProfile.html) in the *Amazon Connect Customer Profiles API Reference*\.

## Parameter object<a name="updatecustomerprofile-parameter"></a>

```
{
    "ProfileRequestData": {
    All of these fields are optional.
       "FirstName",
       "LastName",
       "PhoneNumber",
       "EmailAddress",
       "AccountNumber",
       "Address1",
       "Address2",
       "Address3",
       "Address4",
       "City",
       "Country",
       "County",
       "PostalCode",
       "Province",
       "State"
    },
   "ProfileResponseData": {
       All of these fields are optional.
       "FirstName",
       "LastName",
       "PhoneNumber",
       "EmailAddress",
       "AccountNumber",
       "Address1",
       "Address2",
       "Address3",
       "Address4",
       "City",
       "Country",
       "County",
       "PostalCode",
       "Province",
       "State"
   }
}
```

## Results and conditions<a name="updatecustomerprofile-results"></a>

None\. Conditions are not supported\. If an error does not occur, the response's attributes are available dynamically under the `$.Customer` path based on the attributes included in `ProfileResponseData`\.

## Errors<a name="updatecustomerprofile-errors"></a>
+ NoMatchingError \- if no other Error matches\.

## Corresponding block in the UI<a name="updatecustomerprofile-ui"></a>

[Customer profiles](customer-profiles-block.md)