# Agent Workspace guided experience<a name="step-by-step-guided-experiences"></a>

In the Amazon Connect agent workspace, you can create workflows that walk agents through custom UI pages that suggest what to do at a given moment during a customer interaction\. You can create workflows that give your agents screen pops and single page forms, or you can created detailed step\-by\-step guides that give your agents clear instructions on how to handle a particular use case\. This experience is customizable, both in terms of the data you surface to your agent as well UI that they see\.

To learn more about the possible UI configurations, see our interactive [documentation](https://d2ote8qdyv1arb.cloudfront.net/)\.

To learn more about the pricing of step\-by\-step guides, choose the **Guides** tab on the Amazon Connect [pricing page](https://aws.amazon.com/connect/pricing/)\.

## Overview<a name="step-by-step-guided-experiences-overview"></a>

Agent facing workflows are configured by a creating a contact flow that uses the [Flow block: Show view](show-view-block.md)\. The Show view block determines what View to render in the agent’s UI while all pre\-existing flow blocks can be used to create branching decision trees and send and receive data from external systems\.

When mapping a view to a Show view block, you will be able to select from a list of pre\-built Views\. For more details on the views see [Flow block: Show view](show-view-block.md)\.

## Complex JSON Object support<a name="step-by-step-guided-experiences-complex-json"></a>

The Show view block allows you to pass complex JSON objects between Amazon Connect agent workspaces and flows\. Along with the Show view flow block, the Invoke AWS Lambda flow block is able to take JSON objects as input and output parameters\. This allow you to pass larger quantities of data with fewer mapping steps required\.