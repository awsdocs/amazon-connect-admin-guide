# Use the real\-time analytics API<a name="contact-lens-api"></a>

Use the Contact Lens API [ListRealtimeContactAnalysisSegments](https://docs.aws.amazon.com/contact-lens/latest/APIReference/API_ListRealtimeContactAnalysisSegments.html) to build solutions that make your contact center more efficient\. Following are two use cases for this API\.

## Better call transfers<a name="contact-lens-api-transfers"></a>

When a contact is transferred from one agent to another agent, you can transfer a transcript of the conversation to the new agent\. The new agent then has context for why the customer is calling, and the customer doesn't need to repeat everything they already said\. Use the [ListRealtimeContactAnalysisSegments](https://docs.aws.amazon.com/contact-lens/latest/APIReference/API_ListRealtimeContactAnalysisSegments.html) API to get the entire transcript of the conversation up to a certain point, and share it with the new agent\. 

## Automatic call summaries<a name="contact-lens-api-call-summary"></a>

While handling a call agents may need to make notes, such as listing action items\. Since you have the entire transcript available, you can build machine learning models to identify the key notes and summarize them at the end of the conversation\. These notes are then available for any other agent or supervisor to reference\. This helps agents focus on the conversation and the customer rather than focus on taking notes for the call summary\. 