# Amazon Connect Administrator Guide

-----
*****Copyright &copy; 2019 Amazon Web Services, Inc. and/or its affiliates. All rights reserved.*****

-----
Amazon's trademarks and trade dress may not be used in 
     connection with any product or service that is not Amazon's, 
     in any manner that is likely to cause confusion among customers, 
     or in any manner that disparages or discredits Amazon. All other 
     trademarks not owned by Amazon are the property of their respective
     owners, who may or may not be affiliated with, connected to, or 
     sponsored by Amazon.

-----
## Contents
+ [What Is Amazon Connect?](what-is-amazon-connect.md)
+ [Get Started with Amazon Connect](amazon-connect-get-started.md)
+ [Plan Your Identity Management in Amazon Connect](connect-identity-management.md)
   + [Use an Existing Directory for Identity Management](directory-service.md)
   + [Configure SAML for Identity Management in Amazon Connect](configure-saml.md)
+ [Set Up Your Contact Center](amazon-connect-contact-centers.md)
   + [Create a Virtual Contact Center Instance](amazon-connect-instances.md)
   + [Set Up Phone Numbers for Your Contact Center](contact-center-phone-number.md)
      + [Claim a Phone Number](claim-phone-number.md)
      + [Release a Phone Number](release-phone-number.md)
      + [Port Your Current Phone Number](port-phone-number.md)
      + [Claim Phone Numbers for Amazon Connect in the Asia Pacific (Tokyo) Region](connect-tokyo-region.md)
   + [Set Up Routing](connect-queues.md)
      + [How Routing Works](about-routing.md)
      + [Create a Queue](create-queue.md)
      + [Set the Hours of Operation for a Queue](set-hours-operation.md)
      + [Set Up Outbound Caller ID](queues-callerid.md)
      + [Create a Routing Profile](routing-profiles.md)
   + [Set Up Agents](connect-agents.md)
      + [Set Up Agent Hierarchies](agent-hierarchy.md)
      + [Customize Agent Status Values](agent-status.md)
      + [Configure Agent Settings](configure-agents.md)
   + [Create Amazon Connect Contact Flows](connect-contact-flows.md)
      + [Create a New Contact Flow](create-contact-flow.md)
      + [Associate a Phone Number with a Contact Flow](associate-phone-number.md)
      + [Create Prompts](prompts.md)
      + [Set up Call Transfers](transfer.md)
      + [Set up Call Recording](set-up-recordings.md)
      + [Initiate an Outbound Call](using-call-number-block.md)
      + [Import/Export Contact Flows](contact-flow-import-export.md)
      + [Contact Block Definitions](contact-blocks.md)
      + [Use Amazon Connect Contact Attributes](connect-contact-attributes.md)
   + [Provide Access to the Contact Control Panel](amazon-connect-contact-control-panel.md)
      + [Best Practices for Using the Contact Control Panel](bp-ccp.md)
      + [Amazon Connect Troubleshooting Issues with the CCP](troubleshooting.md)
+ [Add an Amazon Lex Bot](amazon-lex.md)
+ [Invoke Lambda Functions](connect-lambda-functions.md)
+ [Encrypt Customer Input](contact-flow-keys.md)
+ [Capture Customer Audio: Live Media Streaming](customer-voice-streams.md)
   + [Enable Live Media Streaming](enable-live-media-streams.md)
   + [Example Contact Flow for Testing Live Media Streaming](use-media-streams-blocks.md)
   + [Live Media Streaming Contact Attributes](media-streaming-attributes.md)
   + [How to Access Kinesis Video Stream Data](access-media-stream-data.md)
+ [Integrate With Your CRM](crm.md)
   + [Amazon Connect and Salesforce Integration](salesforce-integration.md)
+ [Manage Users in Amazon Connect](connect-security.md)
   + [Add Users](user-management.md)
   + [Reset a User's Password](password-reset.md)
   + [Assign Permissions: Security Profiles](connect-security-profiles.md)
   + [Use Service-Linked Roles for Amazon Connect](connect-slr.md)
+ [Monitoring Amazon Connect](monitoring-amazon-connect.md)
   + [Monitor Live Conversations](monitor-conversations.md)
   + [Review Recorded Conversations](recordings.md)
   + [Login/Logout Reports](login-logout-reports.md)
   + [Amazon Connect Agent Event Streams](agent-event-streams.md)
   + [Contact Flow Logs](contact-flow-logs.md)
   + [CloudWatch Metrics for Your Amazon Connect Instance](monitoring-cloudwatch.md)
+ [Amazon Connect Metrics and Contact Trace Records](amazon-connect-metrics.md)
   + [Real-time Metrics Reports](real-time-metrics-reports.md)
      + [Create a Real-time Metrics Report](create-real-time-report.md)
      + [Download a Real-time Metrics Report](download-real-time-metrics-report.md)
      + [View How Many Customers Are Waiting In Queue](call-back.md)
      + [Real-time Metrics Definitions](real-time-metrics-definitions.md)
   + [Historical Metrics Reports](historical-metrics.md)
   + [Contact Trace Records Data Model](ctr-data-model.md)
+ [Amazon Connect Service Limits](amazon-connect-service-limits.md)
+ [Release Notes](amazon-connect-release-notes.md)
+ [Document History](doc-history.md)