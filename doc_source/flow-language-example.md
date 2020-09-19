# Example contact flow in Amazon Connect Flow language<a name="flow-language-example"></a>

The following example shows a simple contact flow that plays a prompt using static text and disconnects\.

```
{
    "Version": "2019-10-30",  //A string representing the version of the Flow. Currently the only support Version is 2019-10-30.
    "StartAction": "Play prompt identifier", //A string representing the first Action to run when the flow starts running. 
                                            //The value of this field must match with the Identifier of an Action in the Actions list.
    "Metadata": { //An object the may be filled in with data as desired.
        "EntryPointPosition": {
            "X": 88,
            "Y": 100
        },
        "ActionMetadata": {
            "Play prompt identifier": {
                "Position": {
                    "X": 270,
                    "Y": 98
                }
            },
            "Disconnect identifier": {
                "Position": {
                    "X": 545,
                    "Y": 92
                }
            }

        }
    },
    "Actions": [  //A list of individual Action objects. These Actions are the definition of the Flow's behavior and are detailed below. 
                  //A single Flow may have no more than 250 Actions defined.
        {
            "Identifier": "Play prompt identifier",
            "Type": "PlayPrompt",
            "Transitions": {
                "NextAction": "Disconnect identifier",
                "Errors": [],
                "Conditions": []
            },
            "Parameters": {
                "Prompt": {
                    "Text": "Thanks for calling the sample flow!",
                    "TextType": "text",
                    "PromptId": null
                }
            }
        },
        {
            "Identifier": "Disconnect identifier",
            "Type": "Disconnect",
            "Transitions": {},
            "Parameters": {}
        }
    ]
}
```