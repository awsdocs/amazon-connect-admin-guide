# Change behavior of inferred profiles to automatically associate the contact record with one profile found<a name="inferred-profiles-change-behavior"></a>

You can change the behavior of inferred profiles so contact records are automatically associated to one profile found\.

Run the following command on the CLI:

`aws customer-profiles put-profile-object-type --domain-name {domain} --object-type-name CTR --description "No inferred contact record profiles" —template-id CTR-NoInferred`