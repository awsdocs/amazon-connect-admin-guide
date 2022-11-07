# Private optimization APIs<a name="optimization-apis"></a>

Amazon Connect forecasting, capacity planning, and scheduling uses the following private API resources as actions in its IAM policy:
+ `connect:BatchAssociateAnalyticsDataSet`\. Grants access permissions and associates the specified datasets for the specified Amazon Connect instance with the specified AWS account\.
+ `connect:BatchDisassociateAnalyticsDataSet`\. Revokes access permissions and disassociates the specified datasets for the specified Amazon Connect instance with the specified AWS account\.

If you remove these actions from the preview role policy, the forecasting, capacity planning, and scheduling features won't work\.