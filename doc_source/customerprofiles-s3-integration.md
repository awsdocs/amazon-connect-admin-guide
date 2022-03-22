# Example: Programmatically integrate S3 with Customer Profiles<a name="customerprofiles-s3-integration"></a>

Using the Customer Profiles [PutIntegration](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutIntegration.html) API, you can programmatically create integrations for S3, Salesforce, Marketo, and more\. 

In this topic we show how to create an S3 integration with a sync interval of 15 minutes, the minimum value currently supported\. 

## Step 1: Create a JSON file<a name="step1-cpintegration"></a>

Create a JSON file with the following contents:

```
{
    "DomainName": "YOUR-DOMAIN",
    "ObjectTypeName": "YOUR-OBJECT-NAME", 
    "FlowDefinition": {
        "FlowName": "YOUR-FLOW-NAME",
        "KmsArn": "THE KEY ARN IS THE SAME AS YOUR DOMAIN'S KEY",
        "Description": "Created by Customer Profiles",
        "TriggerConfig": {
            "TriggerType": "Scheduled",
            "TriggerProperties": {
                "Scheduled": {
                    "ScheduleExpression": "rate(15minutes)",
                    "DataPullMode": "Incremental",
                    "ScheduleStartTime": 1634244800.435,
                    "FirstExecutionFrom": 1594166400
                }
            }
        },
        "SourceFlowConfig": {
            "ConnectorType":"S3",
            "SourceConnectorProperties": {
                "S3": {
                    "BucketName": "YOUR-BUCKET",
                    "BucketPrefix": "YOUR-PREFIX"
                }
            }
        },
        "Tasks": [
            {"TaskType":"Filter","SourceFields":["colA","colB"],"ConnectorOperator":{"S3":"PROJECTION"}},
            {"ConnectorOperator":{"S3":"NO_OP"},"DestinationField":"colA","TaskProperties":{},"SourceFields":["colA"],"TaskType":"Map"},
            {"ConnectorOperator":{"S3":"NO_OP"},"DestinationField":"colB","TaskProperties":{},"SourceFields":["colB"],"TaskType":"Map"}
        ]
    }
}
```

To customize the JSON with your own values, follow these guidelines:
+ `FlowName`: Can be STRING \[a\-zA\-Z0\-9\]\[\\w\!@\#\.\-\]\+
+ `ScheduleStartTime`: Set to the current `DateTime` \+ 5 minutes in epoch time\.
+ `FirstExecutionFrom`: Go to S3, look at the file date, and use a date that is before the oldest date\.
+ `Tasks`: Define `TaskType`\. In the `Sourcefields` field you have to supply ALL the columns you have in your CSV in that array\. Then, for each of the items in that array, you need to specify the `ConnectorOperator`\. This example is for a CSV document with two columns: `colA` and `colB`\.

## Step 2: Call the PutIntegration API<a name="step2-cpintegration"></a>

After you have created and customized the JSON file with your values, call the [PutIntegration](https://docs.aws.amazon.com/customerprofiles/latest/APIReference/API_PutIntegration.html) API, as shown in the following example:

```
aws customer-profiles put-integration --cli-input-json file:///put_integration_s3_cli.json --region us-west-2                    
```

The response from `PutIntegration` returns a flow URI\. For example:

```
{
    "DomainName": "testDomain",
    "Uri": "arn:aws:appflow:us-west-2:9999999999999:flow/Customer_Profiles_testDomain_S3_Salesforce-Account_1634244122247",
    "ObjectTypeName": "your objec type",
    "CreatedAt": "2021-10-14T13:51:57.748000-07:00",
    "LastUpdatedAt": "2021-10-14T13:51:57.748000-07:00",
    "Tags": {}
}
```

## Step 3: Call the Amazon AppFlow StartFlow API<a name="step3-cpintegration"></a>

Use the flow URI to call the Amazon AppFlow [StartFlow](https://docs.aws.amazon.com/appflow/1.0/APIReference/API_StartFlow.html) API\. For example:

```
aws appflow start-flow —flow-name uri --region us-west-2
```