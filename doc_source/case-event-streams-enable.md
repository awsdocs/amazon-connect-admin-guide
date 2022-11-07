# Set up case event streams<a name="case-event-streams-enable"></a>

This topic explains how to set up and use case event streams\. Some of the onboarding steps require you to call [Amazon Connect Cases APIs](https://docs.aws.amazon.com/cases/latest/APIReference/Welcome.html)\.

## Step 1: Create an Amazon Connect instance and enable Customer Profiles<a name="step1-case-event-streams-enable"></a>

1. Ensure you have an working Amazon Connect instance in the US East \(N\. Virginia\) or US West \(Oregon\) AWS Region\. Cases is available only in US East \(N\. Virginia\) and US West \(Oregon\)\.

   For information about creating an instance, see [Create an Amazon Connect instance](amazon-connect-instances.md)\.

1. Enable Amazon Connect Customer Profiles\. For instructions, see [Enable Customer Profiles for your instance](enable-customer-profiles.md)\.

   Amazon Connect Cases requires Customer Profiles because each case must be associated with a customer profile from the Customer Profiles service\.

## Step 2: Add a Cases domain to your Amazon Connect instance<a name="step2-case-event-streams-enable"></a>

For instructions, see [Enable Cases](enable-cases.md)\.

If you want to add a case domain using the API, see the [CreateDomain](https://docs.aws.amazon.com/cases/latest/APIReference/API_CreateDomain.html) API in the *Amazon Connect Cases API Reference*\. 

## Step 3: Create a case template<a name="step3-case-event-streams-enable"></a>

[Create a case template](case-templates.md)\. In *Step 6: Test case event streams*, you'll use the template\. 

If you want to create a case template using the API, see the [CreateTemplate](https://docs.aws.amazon.com/cases/latest/APIReference/API_CreateTemplate.html) API in the *Amazon Connect Cases API Reference*\. 

## Step 4: Enable case event streams and setup to receive events into an SQS queue<a name="step4-case-event-streams-enable"></a>

Run the following command to enable case event streams for your Cases domain\. After this command runs, when cases are created or updated, an event is published to the default\-bus of the EventBridge service in your account \(it must be in the same AWS Region as your Cases domain\)\.

```
aws connectcases put-case-event-configuration --domain-id dad5efb6-8485-4a55-8241-98a88EXAMPLE --event-bridge enabled=true
```

By default, the events published by Amazon Connect Cases only contain metadata about the case, such as `templateId`, `caseId`, `caseArn`, `approximateChangeTime`, and more\. You can run the following command to get more information about the case \(at the time the event was generated\) to be included in the event\.

**Note**  
If you want to include a custom field in the event, use the custom field ID\. For instructions about how to locate the custom field ID, see [Find the custom field ID](cases-block.md#get-case-properties-find-uuid)\. 

```
# You can include any other field defined in your cases domain in the fields section.
# To list the fields that are defined in your cases domain, call the Cases ListFields API.
# To include case fields that you create (custom fields) in the event, enter the custom field ID.
aws connectcases put-case-event-configuration --domain-id YOUR_CASES_DOMAIN_ID --event-bridge "{
    \"enabled\": true, 
    \"includedData\": {
       \"caseData\": {
          \"fields\": [
          {
          \"id\": \"status\"
          },
          {
          \"id\": \"title\"
          },
          {
          \"id\": \"customer_id\"
          }
         {
          \"id\": \"your custom field ID\"
          },
        ]
      },
      \"relatedItemData\": {
      \"includeContent\": true
      }
    }
  }"
```

Next, create an Amazon SQS queue and set that as a target for the Amazon Connect Cases events on your EventBridge bus so that all the case events are delivered to the SQS queue for later processing\.

```
# Create an SQS queue
aws sqs create-queue --queue-name case-events-queue --attributes "{\"Policy\": \"{ \\\"Version\\\": \\\"2012-10-17\\\", \\\"Statement\\\": [{ \\\"Sid\\\": \\\"case-event-subscription\\\", \\\"Effect\\\": \\\"Allow\\\", \\\"Principal\\\": { \\\"Service\\\": \\\"events.amazonaws.com\\\"}, \\\"Action\\\": \\\"SQS:SendMessage\\\", \\\"Resource\\\": \\\"*\\\"}]}\"}"

# Create an rule on the EventBridge defualt bus that represents the case events
aws events put-rule --name case-events-to-sqs-queue --event-pattern "{\"source\": [\"aws.cases\"]}" --state ENABLED

# Ask event bridge to publish case events to the SQS queue.
aws events put-targets --rule case-events-to-sqs-queue --target "[{
\"Id\": \"target-1\",
\"Arn\": \"arn:aws:sqs:The AWS Region of your Amazon Connect instance:your AWS account ID:case-events-queue\"
}]"
```

## Step 5: Test case event streams<a name="step5-case-event-streams-enable"></a>

Use the Amazon Connect agent application to: 

1. Accept a chat contact\.

1. Create a customer profile and associate that to the chat contact\.

1. Create a case\. 
**Note**  
The **Create case** button on the **Cases** tab is inactive until you accept a contact and associate that contact with a customer profile\.

Navigate to the Amazon SQS console and check that a case event \(type: `CASE.CREATED`\) for the newly created case is available in your SQS Queue\. Similarly, you can modify the case created above and get a corresponding case event \(type: `CASE.UPDATED`\) in your SQS queue\. You can associate the contact to the case, and leave a comment on the case to get case events for those actions, too\.

## Step 6: Use cases for the case event streams<a name="step6-case-event-streams-enable"></a>

Case event streams publish events every time a case is created, case is updated, contact is associated to the case, and comment is added on a case\. You can use these events for:
+ Metrics, analytics and dashboards
+ Build Apps that notify users \(for example, send emails\)
+ Automated actions that are triggered based on certain type of case updates

For example, you can use the SQS target on EventBridge \(as shown on step 4\) to temporarily store the case events in the SQS queue, and use Lambda functions to process events in the SQS to build custom applications such as sending emails to the customer when their case is updated, automatically resolving any tasks linked to the case, and more\. Similarly, you can use the Kinesis Data Firehose target on the EventBridge to store the case events into an S3 bucket and then use the AWS Glue for ETL, Athena for ad\-hoc analytics, and Amazon QuickSight for dashboards\.