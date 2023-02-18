# Example evaluation form output \(Preview\)<a name="evaluationforms-example-output-file"></a>


|  | 
| --- |
| This feature is in preview release and subject to change\.  | 

This section shows the export output path for evaluations, and provides an example of evaluation form scores and metadata\.

## Verify your S3 bucket<a name="verify-evaluation-s3bucket"></a>

When you enable **Contact evaluations** in the Amazon Connect console, you are prompted to create or choose an S3 bucket to store the evaluations\. To verify the name of the bucket, go to your instance alias, choose **Data storage**, **Contact evaluations**, **Edit**\.

## Example output locations<a name="example-evaluationform-output-locations"></a>

Following is the output file path for evaluation forms:
+ *contact\_evaluations\_S3\_bucket*/Evaluations/*YYYY/MM/DD/hh:mm:ss\.sTZD*\-*evaluation\_id*\.json

For example:

`amazon-connect-s3/Evaluations/2022/04/14/05:04:20.869Z-11111111-2222-3333-4444-555555555555.json`

## Known issue: Two output files for the same evaluation<a name="release-note-evaluation-output"></a>

Contact Lens generates two output files for the same evaluation form\.
+ One file is written to the new default S3 path\. You can configure the path in the AWS console\.
+ Another file, which will be deprecated, is written to a different, previous S3 path\. You can disregard this file\.

  The previous S3 path looks like the following:
  + *s3\_bucket*/Evaluations/contact\_*contactId*/evaluation\_*evaluationId*/YYYY\-MM\-DDThh:mm:ss\.sTZD\.json

## Example scores and metadata<a name="example-evaluation-output-file"></a>

```
 {
  "schemaVersion": "3.1",
  "evaluationId": "fb90de35-4507-479a-8b57-970290fd5c2c",
  "metadata": {
    "contactId": "badd4896-75f7-43b3-bee6-c617ed3d04cb",
    "accountId": "874551140838",
    "instanceId": "8f753c94-9cd2-4f16-85eb-945f7f0d559a",
    "agentId": "286bcec0-e722-4166-865f-84db80252218",
    "evaluationDefinitionTitle": "Compliance Evaluation Form",
    "evaluator": "jane",
    "evaluationDefinitionId": "15d8fbf1-b4b2-4ace-869b-82714e2f6e3e",
    "evaluationDefinitionVersion": 2,
    "evaluationStartTimestamp": "2022-11-14T17:57:08.649Z",
    "evaluationSubmitTimestamp": "2022-11-14T17:59:29.052Z",
    "score": { "percentage": 100 }
  },
  "sections": [
    {
      "sectionRefId": "s1a1b58d6",
      "sectionTitle": "The title of the section",
      "notes": "Section note",
      "score": { "percentage": 100 }
    },
    {
      "sectionRefId": "s46661c49",
      "sectionTitle": "The title of the subsection",
      "parentSectionRefId": "s1a1b58d6",
      "score": { "percentage": 100 }
    }
  ],
  "questions": [
    {
      "questionRefId": "q570b206a",
      "sectionRefId": "s46661c49",
      "questionType": "NUMERIC",
      "questionText": "How do you rate the contact between 1 and 10?",
      "answer": {
        "value": "",
        "notes": "Add more information here",
        "metadata": { "notApplicable": true }
      },
      "score": { "notApplicable": true }
    },
    {
      "questionRefId": "q73bc5b9d",
      "sectionRefId": "s46661c49",
      "questionType": "SINGLESELECT",
      "questionText": "Did the agent introduce themselves?",
      "answer": {
        "values": [
          { "valueText": "Yes", "valueRefId": "o6999aa94", "selected": true },
          { "valueText": "No", "valueRefId": "o284e4d9e", "selected": false },
          { "valueText": "Maybe", "valueRefId": "o1b2f0a14", "selected": false }
        ],
        "notes": "Add more information here",
        "metadata": { "notApplicable": false }
      },
      "score": { "percentage": 100 }
    },
    {
      "questionRefId": "qc2effc9d",
      "sectionRefId": "s46661c49",
      "questionType": "TEXT",
      "questionText": "Describe the outcome.",
      "answer": {
        "value": "Example answer text",
        "notes": "Add more information here",
        "metadata": { "notApplicable": false }
      },
      "score": { "notApplicable": true }
    }
  ]
}
```