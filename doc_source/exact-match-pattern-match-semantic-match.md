# How to use exact match, pattern match, and semantic match in a rule<a name="exact-match-pattern-match-semantic-match"></a>

## How to use exact match<a name="exact-match"></a>

**Exact Match** really is an exact word match, singular or plural\.

## How to use pattern match<a name="pattern-match"></a>

If you want to match related words, append an asterisk \(\*\) to the criteria\. For example, if you want to match on all variations of "neighbor" \(neighbors, neighborhood\) you would type **neighbo\***\.

With **Pattern Match** you can specify the following:
+ **List of values**: This is useful when you want to build expressions with interchangeable values\. For example, the expression might be: 

  *I'm calling about a power outage in \["Beijing" or "London" or "New York" or "Paris" or "Tokyo"\]*

  Then in your list of values you would add the cities: Beijing, London, New York, Paris, Tokyo\. 

  The advantage of using values is that you can create one expression, instead of multiple\. This reduces the number of cards that you need to create\.
+ **Number**: This option is used most frequently in compliance scripts, or if your looking for a context when you know somewhere in between there's a number\. This way you can put all of your criteria into one expression instead of two\. For example, an agent compliance script might say:

  *I have been in this industry for \[num\] years and would like to discuss this topic with you\.*

  Or a customer might say: 

  *I have been a member for \[num\] years\.*
+ **Proximity definition**: Finds matches that may be less than 100 percent exact\. You can also specify the distance between words\. For example, if you are looking for contacts where the word "credit" was mentioned but you do not want to see any mention of the words "credit card," you can define a pattern matching category to look for the word "credit" that is not within a one\-word distance of "card\."

  For example, a proximity definition might be:

  *credit\* \[is not within 0 to 1 word apart\] card\**

**Tip**  
For a list of languages supported by pattern match, see [Pattern match languages](supported-languages.md#supported-languages-contact-lens-pattern-matching)\. 

## How to use semantic match<a name="semantic-match"></a>

Semantic matching is supported only for post\-call analysis\.
+ An “intent” is an example of utterance\. It can be a phrase or a sentence\.
+ You can enter up to four intents in one card \(group\)\.
+ We recommend using semantically similar intents within one card to get the best results\. For example, there's category for "politeness\." It includes two intents: "greetings" and "goodbye"\. We recommend separating these intents into two cards:
  + Card 1: "How are you today" and "How’s everything going"\. They are semantically similar greetings\.
  + Card 2: "Thanks for contacting us" and "Thank you for being our customer\." They are semantically similar goodbyes\.

  Separating the intents into two cards provides more accuracy than putting them all into one card\.