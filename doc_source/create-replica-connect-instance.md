# Create a replica of your existing Amazon Connect instance<a name="create-replica-connect-instance"></a>

**Note**  
This feature is available only for Amazon Connect instances created in the US East \(N\. Virginia\) and US West \(Oregon\) Regions\.   
To obtain access to this feature, contact your Amazon Connect Solutions Architect or Technical Account Manager\.

You call the [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API to create a replica of your Amazon Connect instance in another AWS Region\.

Before using [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) to create a replica, make sure you have the minimum required IAM permissions to create an instance\. See [Required permissions for using custom IAM policies to manage access to the Amazon Connect console](security-iam-amazon-connect-permissions.md)\.

## Characteristics of the replica instance<a name="replica-characteristics"></a>
+ The replica Amazon Connect instance is created in the same AWS account as your existing Amazon Connect instance\.
+ The replica instance is empty initially except for the default resources that are always created with an instance\.
+ The replica has the same instance ID as the Amazon Connect instance it is replicated from\.

## Configure the replica instance<a name="configure-replica-instance"></a>

After your replica Amazon Connect instance is created, you need to configure it:

1. Ensure SAML is enabled in the replica Amazon Connect instance\.

1. Mirror the configuration of Amazon Connect resource across Regions if needed\. For example, users, routing profiles, queues, and flows\.

1. Ensure redundancy for front\-end and back\-end integrations \(for example, SSO, Lambda, Lex\) across Regions\.

1. Make matching manual updates across the linked instances\.

## Why a ReplicateInstance call fails<a name="why-replicateinstance-fails"></a>

A [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API call fails with an `InvalidRequestException` in the following cases:

1. The Region where you are creating the replica is the same Region as your existing instance\.

1. The instance was already replicated as part of a different [ReplicateInstance](https://docs.aws.amazon.com/connect/latest/APIReference/API_ReplicateInstance.html) API call\.

1. The instance does not have an alias\.

1. The instance is not in `ACTIVE` status\.

1. The instance does not have SAML enabled\.