# GetCustomerProfile<a name="interactions-getcustomerprofile"></a>

Retrieve a customer profile based on email or phone number\. Customer Profiles must be enabled for your Amazon Connect instance\.

See [SearchProfiles](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_SearchProfiles.html) in the *Amazon Connect Customer Profiles API Reference*\.

## Parameter object<a name="getcustomerprofile-parameter"></a>

A search key \(phone number or email\) must be present\.

```
{
    "ProfileRequestData": {
       "PhoneNumber": Phone number to search for profiles with.
       "EmailAddress": Email address to search for profiles with.
    },
   "ProfileResponseData": {
       All of these fields are optional.
       Profile ID, if a single profile is found, is always persisted under the Customer -> ProfileID attribute + $.Customer.ProfileId
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

## Results and conditions<a name="getcustomerprofile-results"></a>

None\. Conditions are not supported\. If an error does not occur, the response's attributes are available dynamically under the `$.Customer` path based on the attributes included in `ProfileResponseData`\.

## Errors<a name="getcustomerprofile-errors"></a>
+ MultipleFoundError \- if multiple profiles were found for the associated profile search key\.
+ NoneFoundError \- if no profiles were found for the associated profile search key\.
+ NoMatchingError \- if no other Error matches\.

## Corresponding block in the UI<a name="getcustomerprofile-ui"></a>

[Customer profiles](customer-profiles-block.md)