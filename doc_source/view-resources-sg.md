# View resource \(Preview\)<a name="view-resources-sg"></a>


|  | 
| --- |
| This is prerelease documentation for a service in preview release\. It is subject to change\. | 

Views are UI templates that you can use to customize your agent’s workspace\. For example, you can use Views to display contact attributes to an agent, provide forms for entering disposition codes, provide call notes, and present UI pages for walking agents through step\-by\-step guides\. Amazon Connect comes with a set of Views that you can add your agent’s workspace by using the Show View block in Connect Flows\. Each View is configurable and you can see how by clicking on the below tabs\.

For the best data mapping experience, we recommend using the **Set JSON** option in the Show View flow block\. All namespaces in Flows can be referenced in the Show View block, including `$.External`, so you will be able to share data from external systems to your agent in whichever View you create\. You can mix and match data from Amazon Connect and other sources in order to create a consolidated UI for your agent\.

For more information on the Flows **Show view** block, see [Show view \(Preview\)](https://docs.aws.amazon.com/connect/latest/adminguide/show-view-block.html)\.

------
#### [ Details view ]

The detail view is for displaying information to the agent and providing them with a list of actions that they can take\. A common use case of the **Detail view** is to surface a screen\-pop to the agent at the start of a call\. Actions in this view can be used to let an agent continue to the next step in a step\-by\-step guide or the actions can be used to invoke entirely new workflows\. Optional components such as the **AttributeBar** are supported by this view, but the only required component is **Sections** which is where you can configure the body of the page you want to show to your agent\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/details-view-page-heading-sq.png)

**Sections**
+ Optional, if provided will display the sections provided\.
+ Content can be a static string, a Template String or a key\-value pair\. It can be a single data point or a list\.

**AttributeBar \(Optional\)**
+ Optional, if provided will display the Attribute bar at the top of the view\.
+ Is a list of objects with required properties, **Label**, **Value**, and optional properties **LinkType**, **ResourceId**, **Copyable** and **Url**\.
  + **LinkType** can be external or connect application such as case\.
    + When it is *external*, a user can navigate to a new browser page, which is configured with **Url**\.
    + When it is *case*, a user can navigate to a new case detail on the Agent workspace, which configured with ResourceId\.
  + **Copyable** allows users to copy the ResourceId by choosing it with your input device\.

**Back \(Optional\)**
+ Optional, but required if no actions are included\. if provided will display the back navigation link\.
+ Is an object with a *Label* which will control what is displayed in the link text\.

**Heading \(Optional\)**
+ Optional, if provided will display Text as the title\.

**Description \(Optional\)**
+ Optional, if provided will display description text under the title\.

**Actions \(Optional\)**
+ Optional\. If provided, will display a list of action at the bottom of the page\.

**Input data**

```
{
  "AttributeBar": [
    {"Label": "Example", "Value": "Attribute"},
    { "Label": "Example 2", "Value": "Attribute 3", "LinkType": "case", "ResourceId": "123456", "Copyable": true }
  ],
  "Back": {
    "Label": "Back"
  },
  "Heading": "Hello world",
  "Description": "This view is showing off the wonders of a detail page",
  "Sections": [{
    "TemplateString": "This is an intro paragraph"
  }, "abc"],
  "Actions": ["Do thing!", "Update thing 2!"],
}
```

**Output data**

```
{
    Action: "ActionSelected",
    Output: {
        actionName: "Update thing 2!"
    }
}
```

**Input data schema**

```
{
  "AttributeBar": [
    {"Label": "Queue", "Value": "Sales"},
    {"Label": "Case ID", "Value": { "ExternalLink": {"Url": "https://...", "Label": "1234567"}}},
    {"Label": "Case", "Value": "New reservation"}
  ],
  "PrimaryPageNav": {
    "Label": "Back to Home"
  },
  "Title": "Page Title",
  "Description": "Description of package or ...",
  "Content": {
    "TemplateString": ...
  },
  "Actions": ["Action 1", "Action 2", "Action 3", {"ExternalAction": {"Url": ...., "Label": "Go Somewhere"}}]  
}
```

------
#### [ List view ]

The list view is for displaying information as a list of items with titles and descriptions\. Items may also act as links, with actions attached\. It also optionally supports the standard back navigation and persistent context header\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/list-view-column-sq.png)

**Items**
+ Required, will display these items as a list\.
+ Each item may have a Heading, Description, Icon, and Id\.
  + All properties are optional\.
  + When Id is defined, the output will include the value as part of output\.

**AttributeBar \(Optional\)**
+ Optional, if provided will display the Attribute bar at the top of the view\.
+ Is a list of objects with required properties, **Label**, **Value**, and optional properties **LinkType**, **ResourceId**, **Copyable** and **Url**\.
  + **LinkType** can be external or connect application such as case\.
    + When it is *external*, a user can navigate to a new browser page, which is configured with **Url**\.
    + When it is *case*, a user can navigate to a new case detail on the Agent workspace, which configured with ResourceId\.
  + **Copyable** allows users to copy the ResourceId by choosing it with your input device\.

**Back \(Optional\)**
+ Optional, but required if no actions are included\. if provided will display the back navigation link\.
+ Is an object with a *Label* which will control what is displayed in the link text\.

**Heading \(Optional\)**
+ Optional, if provided will display Text as the title\.

**SubHeading \(Optional\)**
+ Optional, if provided will display Text as the title of list\.

**Input data Schema**

```
                            {
  "AttributeBar": [
    {"Label": "Queue", "Value": "Sales"},
    {"Label": "Case ID", "Value": { "ExternalLink": {"Url": "https://...", "Label": "1234567"}}},
    {"Label": "Case", "Value": "New reservation"}
  ],
  "PrimaryPageNav": {
    "Label": "Back to Home"
  },
  "Title": "List Title",
  "Items": [
    {
      "header": "Item 1",
      "subHeader": "This is a description",
      "icon": "Hospital",
      "action": "Click_Item1"
    },
    {
      "header": "Item 2",
      "subHeader": "This is a description"
    },
    {
      "header": "Item 3",
      "action": "Click_Item3"
    }
  ],
  "Actions": ["Action 1", "Action 2", "Action 3"]  
}
```

------
#### [ Form view ]

The Form view allows you to provide your agents with custom forms that meet your unique use cases\. Basic types of input fields are supported and you’ll be able to submit data to homegrown or 3rd party systems by integrating with the Lambda flow block in the Flows editor\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/form-view-sq.png)

**Heading**
+ String, Form view main title\.

**SubHeading**
+ String, Form view subtitle shown just below *Title*\.

**Sections**
+ Section layout information, object with \_id, Type, Items, Heading\.
+ **\_Id**
  + Unique identifier for the group\.
+ **Heading**
  + Title of the group of forms or attributes\.
+ **Type**
  + Type of Form: either `FormSection` \(forms handling user's input\) or `Attributes` \(displaying a list of label and value\)\.
+ **Items**
  + Array of Form Section objects\. Each Form Section object will have \_id, Heading and Items along with default LayoutConfiguration\.
    + **LayoutConfiguration** Object which accepts Grids\.
      + Grid will be a list of colspan \(each columns information\)\.
        + colspan includes the column size per screen size\. \(Supported screen size: default, xs\)
    + **Items** Array of Form Field items that are two dimensional\.
      + Type \- type of the form field, Allowed fields include DatePicker, TimePicker, Dropdown and more\.
      + Label \- label of the form field\.
      + Name \- Form field name, when the value is returned, it will be the key of the value\.
      + DefaultValue \- Initial Value set for the form field set\.
      + Fluid \- Optional, whether or not the input has full width\. The default is *false*\.
      + Required \- Optional, whether or not the input is required\. The label will have `"*"`\.
      + ShowErrors \- Optional, whether or not it shows an error message\.
      + InputType \- when Type is FormInput, it sets the type of form input\. The default is *text*\.
        + supported values: `number`, `text`, `password`, `email`, `tel`, `url`\.
      + Options \- a list of options for multiple choices such as Dropdown, CheckboxGroup, or RadioGroup\. Should be a list of objects \(Label and Value\)
      + MultiSelect \- when Type is Dropdown, it allows a user to select multiple options\. The default is *false*\.

**Next**
+ Type Object, expects optional Label String and optional Details object which is a free form Object that gets sent in parallel with Form dynamic data using the Action Name **Submit**\.

**Cancel**
+ Type Object, expects optional Label String and optional Details object which is a free form Object that gets sent in parallel with the **Cancel** action\.

**Back**
+ Required
+ Object with keys:
  + Label \- string label for the navigation button\.

**AttributeBar \(Optional\)**
+ Optional, if provided will display the Attribute bar at the top of the view\.
+ Is a list of objects with required properties, **Label**, **Value**, and optional properties **LinkType**, **ResourceId**, **Copyable** and **Url**\.
  + **LinkType** can be external or connect application such as case\.
    + When it is *external*, a user can navigate to a new browser page, which is configured with **Url**\.
    + When it is *case*, a user can navigate to a new case detail on the Agent workspace, which configured with ResourceId\.
  + **Copyable** allows users to copy the ResourceId by choosing it with your input device\.

**ErrorText \(Optional\)**
+ Optional, shows server\-side error messages\.
+ Expect Heading and Content\.

**Input data Schema**

```
                            {
  "PrimaryPageNav": {
    "Label": "Back Home"
  },
  "Submit": {
    "Label": "Confirm Reservation",
    "Details": {
      "endpoint": "awesomecustomer.com/submit",
      "additionalparams": {
        "Agent": "jagadeey"
      }
    }
  },
  "Cancel": {
    "Label": "Cancel"
  },
  "AttributeBar": [
    {
      "Label": "Attribute1",
      "Value": "Value1"
    },
    {
      "Label": "Attribute2",
      "Value": "Value2"
    },
    {
      "Label": "Attribute3",
      "Value": "Value3"
    },
    {
      "Label": "Attribute4",
      "Value": "Value4"
    }
  ],
  "Title": "Modify Reservation",
  "SubTitle": "Cadillac XT5",
  "ErrorText": {
    "Header": "Modify reservation failed",
    "Content": "Internal Server Error, please try again"
  },
  "Sections": [
    {
      "_id": "pickup",
      "Title": "Pickup Details",
      "Items": [
        {
          "LayoutConfiguration": {
            "Grid": [
              {
                "colspan": {
                  "default": 12,
                  "xs": 6
                }
              }
            ]
          },
          "Items": [
            {
              "Type": "FormInput",
              "Fluid": true,
              "InputType": "search",
              "Label": "Location",
              "Name": "pickup-location",
              "DefaultValue": "Seattle",
              "Values": [
                {},
                {},
                {}
              ],
              "Required": true
            }
          ]
        },
        {
          "LayoutConfiguration": {
            "Grid": [
              {
                "colspan": {
                  "default": 6,
                  "xs": 4
                }
              },
              {
                "colspan": {
                  "default": 6,
                  "xs": 4
                }
              }
            ]
          },
          "Items": [
            {
              "Label": "Day",
              "Type": "FormInput",
              "InputType": "date",
              "Fluid": true,
              "DefaultValue": "2022-10-10",
              "Name": "pickup-day",
              "Required": true
            },
            {
              "Label": "Time",
              "Type": "FormInput",
              "InputType": "time",
              "Fluid": true,
              "DefaultValue": "13:00",
              "Name": "pickup-time"
            }
          ]
        }
      ]
    },
    {
      "_id": "dropoff",
      "Title": "Drop off details",
      "Items": [
        {
          "LayoutConfiguration": {
            "Grid": [
              {
                "colspan": {
                  "default": 12,
                  "xs": 6
                }
              }
            ]
          },
          "Items": [
            {
              "Label": "Location",
              "Type": "FormInput",
              "Fluid": true,
              "DefaultValue": "Lynnwood",
              "Name": "dropoff-location",
              "Required": true
            }
          ]
        },
        {
          "LayoutConfiguration": {
            "Grid": [
              {
                "colspan": {
                  "default": 6,
                  "xs": 4
                }
              },
              {
                "colspan": {
                  "default": 6,
                  "xs": 4
                }
              }
            ]
          },
          "Items": [
            {
              "Label": "Day",
              "Type": "FormInput",
              "InputType": "date",
              "Fluid": true,
              "DefaultValue": "2022-10-15",
              "Name": "dropoff-day",
              "Required": true
            },
            {
              "Label": "Time",
              "Type": "FormInput",
              "InputType": "time",
              "Fluid": true,
              "DefaultValue": "01:00",
              "Name": "dropoff-time"
            }
          ]
        }
      ]
    }
  ]
}
```

------
#### [ Wizard view ]

The Wizard view lets you create a multi\-step process for your agents\. One example use case would be to create a multi\-page form that lets your agent focus on one task at a time as they gather information from an end\-customer\. Just like the Form view, you will be able to enable input fields unique to your use case\. All data submitted by a Wizard form can also be sent to homegrown and 3rd party solutions via the Lambda block in Flows\.

**Example UI**

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/wizard-view-sq.png)

**Heading**
+ String, Wizard view, main title\.

**Steps**
+ Required, will display ProgressTracker at the left side of the View\.
+ Is a list of objects with Heading, Selected, Optional and \_id\.
  + Heading , shows along side with content\.
  + Selected, shows current stage of wizard, if not given defaults to false\.
  + Optional, shows flag for optional\.

**StepSection**
+ Current step view information\.
+ Required, Object with \_id, Title and Content
  + **\_Id** Unique identifier for the section, shows the relationship between step and stepSection\.
    + When the \_id points to the last step, action button shows "Submit" for the next view, not "Next"\.
    + when the \_id doesn’t point to the last step, action button shows "Next" for the next view\.
  + **Heading** Title of the section\.
  + **Content** Section layout information, object with \_id, Type, Items, Heading\.
    + **\_Id** Unique identifier for the group\.
    + **Heading** Title of the group of forms or attributes\.
    + **Type** Type of Form: either FormSection\(forms handling user's input\) or Attributes\(displaying a list of label and value\)\.
    + **Items** Array of Form Section objects\. Each Form Section object will have \_id, Heading and Items along with default LayoutConfiguration\.
      + **LayoutConfiguration** Object which takes Grids\.
        + Grid will be a list of colspan \(each columns information\)\.
          + colspan includes the column size per screen size \(Supported screen size: default, XS\)\.
      + **Items** Array of Form Field items \(2 dimensional\)\.
        + Type \- type of the form field, Allowed fields include DatePicker, TimePicker, Dropdown and more\.
        + Label \- label of the form field\.
        + Name \- Form field name, when the value is returned, it will be the key of the value\.
        + DefaultValue \- Initial Value set for the form field set\.
        + Fluid \- Optional, whether or not the input has full width\. The default is *false*\.
        + Required \- Optional, whether or not the input is required\. The label will have `"*"`\.
        + ShowErrors \- Optional, whether or not it shows an error message\.
        + InputType \- when Type is FormInput, it sets the type of form input\. The default is *text*\.
          + supported values: `number`, `text`, `password`, `email`, `tel`, `url`\.
        + Options \- a list of options for multiple choices such as Dropdown, CheckboxGroup, or RadioGroup\. Should be a list of objects \(Label and Value\)
        + MultiSelect \- when Type is Dropdown, it allows a user to select multiple options\. The default is *false*\.

**Back**
+ Required
+ Object with keys:
  + Label \- string label for the navigation button\.

**AttributeBar \(Optional\)**
+ Optional, if provided will display the Attribute bar at the top of the view\.
+ Is a list of objects with required properties, **Label**, **Value**, and optional properties **LinkType**, **ResourceId**, **Copyable** and **Url**\.
  + **LinkType** can be external or connect application such as case\.
    + When it is *external*, a user can navigate to a new browser page, which is configured with **Url**\.
    + When it is *case*, a user can navigate to a new case detail on the Agent workspace, which configured with ResourceId\.
  + **Copyable** allows users to copy the ResourceId by choosing it with your input device\.

**ErrorText \(Optional\)**
+ Optional, shows server\-side error messages\.
+ Expect Heading and Content\.

**Cancel \(Optional\)**
+ Optional, default is Cancel\.
+ Type Object, expects optional Label String and optional Details object which is a free form Object which gets sent along side with Cancel Action\.

**Next \(Optional\)**
+ Optional, default is Next\.
+ This action is used when the step is not the last step in steps\.
+ Type Object, expects optional Label String and optional Details object which is a free form Object which gets sent along side with Cancel Action\.

**Previous \(Optional\)**
+ Optional, default is Previous\.
+ This action is used when the step is not the first step\.
+ Type Object, expects optional Label String and optional Details object which is a free form Object which gets sent along side with Cancel Action\.

**Edit \(Optional\)**
+ Optional, default is Edit\.
+ This action is used when the section type is *Attributes*\.
+ Type Object, expects optional Label String and optional Details object which is a free form Object which gets sent along side with Cancel Action\.

**Input Data Example**

```
 {
    "AttributeBar": [{
        "Label": "Queue",
        "Value": "Sales"
    }, {
        "Label": "Case ID",
        "Value": "1234567"
    }, {
        "Label": "Case",
        "Value": "New reservation"
    }, {
        "Label": "Attribute  3",
        "Value": "Attribute"
    }],
    "Steps": [{
        "Heading": "Pick up and drop off",
        "_id": "pickup_dropoff",
        "Selected": true
    }, {
        "Heading": "Review and submit",
        "_id": "review_submit"
    }],
    "StepSection": {
        "Heading": "Pick up and drop off",
        "_id": "pickup_dropoff",
        "Content": [{
            "_id": "pickup",
            "Type": "FormSection",
            "Heading": "Pickup Details",
            "Items": [{
                "LayoutConfiguration": {
                    "Grid": [{
                        "colspan": {
                            "default": "12",
                            "xs": "6"
                        }
                    }]
                },
                "Items": [{
                    "Type": "FormInput",
                    "Fluid": true,
                    "InputType": "text",
                    "Label": "Location",
                    "Name": "pickup-location",
                    "DefaultValue": "Seattle"
                }]
            }, {
                "LayoutConfiguration": {
                    "Grid": [{
                        "colspan": {
                            "default": "6",
                            "xs": "4"
                        }
                    }, {
                        "colspan": {
                            "default": "6",
                            "xs": "4"
                        }
                    }]
                },
                "Items": [{
                    "Label": "Day",
                    "Type": "DatePicker",
                    "Fluid": true,
                    "DefaultValue": "2022-11-02",
                    "Name": "pickup-day"
                }, {
                    "Label": "Time",
                    "Type": "TimeInput",
                    "Fluid": true,
                    "DefaultValue": "13:00",
                    "Name": "pickup-time"
                }]
            }]
        }, {
            "_id": "dropoff",
            "Heading": "Drop off details",
            "Type": "FormSection",
            "Items": [{
                "LayoutConfiguration": {
                    "Grid": [{
                        "colspan": {
                            "default": "12",
                            "xs": "6"
                        }
                    }]
                },
                "Items": [{
                    "Label": "Location",
                    "Type": "FormInput",
                    "Fluid": true,
                    "DefaultValue": "Lynnwood",
                    "Name": "dropoff-location"
                }]
            }, {
                "LayoutConfiguration": {
                    "Grid": [{
                        "colspan": {
                            "default": "6",
                            "xs": "4"
                        }
                    }, {
                        "colspan": {
                            "default": "6",
                            "xs": "4"
                        }
                    }]
                },
                "Items": [{
                    "Label": "Day",
                    "Type": "DatePicker",
                    "Fluid": true,
                    "DefaultValue": "2022-11-10",
                    "Name": "dropoff-day"
                }, {
                    "Label": "Time",
                    "Type": "TimeInput",
                    "Fluid": true,
                    "DefaultValue": "01:00",
                    "Name": "dropoff-time"
                }]
            }]
        }]
    },
    "Back": {
        "Label": "Back"
    },

    "ErrorText": {
        "Heading": "Modify reservation failed",
        "Content": "Internal Server Error, please try again"
    },
    "Cancel": {
        "Label": "Cancel"
    },
    "Next": {
        "Label": "Next"
    },
    "Previous": {
        "Label": "Previous"
    },
    "Edit": {
        "Label": "Edit"
    }
    "Heading": "Hotel reservation",
}
```

**Output Data Example**

```
 
{
    Action: "Next",
    Output: {
        ActionOutput: {
            formData: {
                "dropoff-day": "2022-10-15",
                "dropoff-location": "Lynnwood",
                "dropoff-time": "01:00",
                "pickup-day": "2022-10-10",
                "pickup-location": "Seattle"
                "pickup-time": "13:00"
            }
        },
        Label: "Submit"
    }
}
```

**Input Data Schema**

```
{
   "type":"object",
   "properties":{
      "AttributeBar":{
         "type":"array",
         "items":{
            "type":"object",
            "properties":{
               "Label":{
                  "type":"string"
               },
               "Value":{
                  "type":"string"
               }
            },
            "required":[
               "Label",
               "Value"
            ]
         }
      },
      "Heading":{
         "type":"string"
      },
      "Back":{
         "$ref":"#/$defs/Action"
      },
      "Previous":{
         "$ref":"#/$defs/Action"
      },
      "Cancel":{
         "$ref":"#/$defs/Action"
      },
      "Edit":{
         "$ref":"#/$defs/Action"
      },
      "Next":{
         "$ref":"#/$defs/Action"
      },
      "Steps":{
         "type":"array",
         "items":{
            "type":"object",
            "properties":{
               "Heading":{
                  "type":"string"
               },
               "Selected":{
                  "type":"boolean"
               },
               "_id":{
                  "type":"string"
               }
            },
            "required":[
               "Heading",
               "_id"
            ]
         }
      },
      "StepSection":{
         "type":"object",
         "properties":{
            "Heading":{
               "type":"string"
            },
            "_id":{
               "type":"string"
            },
            "Content":{
               "type":"array",
               "items":{
                  "type":"object",
                  "properties":{
                     "_id":{
                        "type":"string"
                     },
                     "Heading":{
                        "type":"string"
                     },
                     "Type":{
                        "type":"string",
                        "enum":[
                           "FormSection",
                           "Attributes"
                        ]
                     },
                     "Total":{
                        "type":"object",
                        "properties":{
                           "Value":{
                              "type":"string"
                           },
                           "Label":{
                              "type":"string"
                           }
                        }
                     },
                     "IsEditable":{
                        "type":"boolean"
                     },
                     "LayoutConfiguration":{
                        "$ref":"#/$defs/LayoutConfiguration"
                     },
                     "Items":{
                        "type":"array",
                        "items":{
                           "type":"object",
                           "properties":{
                              "Items":{
                                 "type":"array",
                                 "items":{
                                    "anyOf":[
                                       {
                                          "$ref":"#/$defs/FormItem"
                                       },
                                       {
                                          "$ref":"#/$defs/AttributeItem"
                                       }
                                    ]
                                 }
                              },
                              "LayoutConfiguration":{
                                 "$ref":"#/$defs/LayoutConfiguration"
                              }
                           },
                           "required":[
                              "Items"
                           ]
                        }
                     }
                  },
                  "required":[
                     "_id",
                     "Heading",
                     "Type",
                     "Items"
                  ]
               }
            }
         },
         "required":[
            "Heading",
            "_id",
            "Content"
         ]
      },
      "ErrorText":{
         "anyOf":[
            {
               "type":"string"
            },
            {
               "type":"object",
               "properties":{
                  "Heading":{
                     "type":"string"
                  },
                  "Content":{
                     "type":"string"
                  }
               },
               "required":[
                  "Heading",
                  "Content"
               ]
            }
         ]
      }
   },
   "$defs":{
      "FormItem":{
         "anyOf":[
            {
               "$ref":"#/$defs/BasicInputFields"
            },
            {
               "$ref":"#/$defs/Checkbox"
            },
            {
               "$ref":"#/$defs/RadioCheckboxGroup"
            },
            {
               "$ref":"#/$defs/Dropdown"
            },
            {
               "$ref":"#/$defs/Address"
            },
            {
               "$ref":"#/$defs/Toggle"
            },
            {
               "$ref":"#/$defs/TextArea"
            }
         ]
      },
      "AttributeItem":{
         "type":"object",
         "properties":{
            "Label":{
               "type":"string"
            },
            "Value":{
               "type":"string"
            },
            "Name":{
               "type":"string"
            }
         }
      },
      "BasicInputFields":{
         "type":"object",
         "properties":{
            "Label":{
               "type":"string"
            },
            "Name":{
               "type":"string"
            },
            "DefaultValue":{
               "type":"string"
            },
            "HelperText":{
               "type":"string"
            },
            "Required":{
               "type":"boolean"
            },
            "showErrors":{
               "type":"boolean"
            },
            "Fluid":{
               "type":"boolean"
            },
            "Type":{
               "type":"string",
               "enum":[
                  "DatePicker",
                  "TimeInput",
                  "FormInput"
               ]
            },
            "InputType":{
               "type":"string",
               "enum":[
                  "number",
                  "text",
                  "password",
                  "email",
                  "tel",
                  "url"
               ]
            }
         },
         "required":[
            "Label",
            "Name"
         ]
      },
      "Checkbox":{
         "type":"object",
         "properties":{
            "name":{
               "type":"string"
            },
            "Type":{
               "type":"string",
               "enum":[
                  "Checkbox"
               ]
            },
            "label":{
               "type":"string"
            },
            "value":{
               "type":"boolean"
            }
         },
         "required":[
            "name",
            "label"
         ]
      },
      "RadioCheckboxGroup":{
         "type":"object",
         "properties":{
            "Name":{
               "type":"string"
            },
            "Type":{
               "type":"string",
               "enum":[
                  "CheckboxGroup",
                  "RadioGroup"
               ]
            },
            "Label":{
               "type":"string"
            },
            "DefaultValue":{
               "type":"string"
            },
            "Options":{
               "type":"array",
               "items":{
                  "type":"object",
                  "properties":{
                     "Value":{
                        "type":"string"
                     },
                     "Label":{
                        "type":"string"
                     },
                     "Description":{
                        "type":"string"
                     }
                  }
               }
            }
         },
         "required":[
            "Name",
            "Label"
         ]
      },
      "Dropdown":{
         "type":"object",
         "properties":{
            "Name":{
               "type":"string"
            },
            "Label":{
               "type":"string"
            },
            "DefaultValue":{
               "type":"array"
            },
            "MultiSelect":{
               "type":"boolean"
            },
            "Options":{
               "type":"array",
               "items":{
                  "type":"object",
                  "properties":{
                     "Value":{
                        "type":"string"
                     },
                     "Label":{
                        "type":"string"
                     }
                  }
               }
            },
            "Required":{
               "type":"boolean"
            },
            "showErrors":{
               "type":"boolean"
            }
         },
         "required":[
            "Name",
            "Label",
            "Options"
         ]
      },
      "Address":{
         "type":"object",
         "properties":{
            "Name":{
               "type":"string"
            },
            "DefaultValue":{
               "type":"object",
               "properties":{
                  "Address":{
                     "type":"string"
                  },
                  "City":{
                     "type":"string"
                  },
                  "State":{
                     "type":"string"
                  },
                  "Country":{
                     "type":"string"
                  },
                  "Zip":{
                     "type":"string"
                  }
               }
            },
            "showErrors":{
               "type":"boolean"
            }
         },
         "required":[
            "Name"
         ]
      },
      "Action":{
         "type":"object",
         "properties":{
            "Label":{
               "type":"string"
            },
            "Details":{
               
            }
         },
         "required":[
            "Label"
         ]
      },
      "LayoutConfiguration":{
         "type":"object",
         "properties":{
            "Grid":{
               "anyOf":[
                  {
                     "type":"array",
                     "items":{
                        "type":"object",
                        "properties":{
                           "colspan":{
                              "type":"string"
                           }
                        }
                     }
                  },
                  {
                     "type":"array",
                     "items":{
                        "type":"object",
                        "properties":{
                           "colspan":{
                              "type":"object",
                              "properties":{
                                 "default":{
                                    "type":"string"
                                 },
                                 "xxs":{
                                    "type":"string"
                                 },
                                 "xs":{
                                    "type":"string"
                                 },
                                 "s":{
                                    "type":"string"
                                 },
                                 "m":{
                                    "type":"string"
                                 },
                                 "l":{
                                    "type":"string"
                                 },
                                 "xl":{
                                    "type":"string"
                                 },
                                 "xxl":{
                                    "type":"string"
                                 }
                              }
                           }
                        }
                     }
                  }
               ]
            },
            "ColumnLayout":{
               "type":"object",
               "properties":{
                  "columns":{
                     "type":"string"
                  },
                  "borders":{
                     "type":"string",
                     "enum":[
                        "vertical",
                        "horizontal",
                        "all"
                     ]
                  },
                  "variant":{
                     "type":"string",
                     "enum":[
                        "default",
                        "text-grid"
                     ]
                  }
               },
               "required":[
                  "columns"
               ]
            }
         }
      },
      "Toggle":{
         "type":"object",
         "properties":{
            "Name":{
               "type":"string"
            },
            "Label":{
               "type":"string"
            },
            "DefaultValue":{
               "type":"boolean"
            }
         },
         "required":[
            "Name"
         ]
      },
      "TextArea":{
         "type":"object",
         "properties":{
            "Name":{
               "type":"string"
            },
            "Label":{
               "type":"string"
            },
            "DefaultValue":{
               "type":"string"
            },
            "Required":{
               "type":"boolean"
            },
            "showErrors":{
               "type":"boolean"
            }
         },
         "required":[
            "Name"
         ]
      }
   },
   "required":[
      "Heading",
      "Steps",
      "StepSection"
   ]
}
```

------
#### [ Confirmation view ]

The confirmation page view is a page to show users after a form has been submitted or an action has been completed that summarizes what has happened, any next steps, or prompts\. Confirmation page supports the persistent attribute bar, an icon / image, Headline and sub\-headline, along with a back to home navigation button\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/confirmation-view-check-sq.png)

**Heading**
+ Required\.
+ Primary message for the confirmation page\.
+ Text only\.

**Next**
+ Required\.
+ Object with keys:
  + Label \- string label for the navigation button\.

**AttributeBar \(Optional\)**
+ Optional, if provided will display the Attribute bar at the top of the view\.
+ Is a list of objects with required properties, **Label**, **Value**, and optional properties **LinkType**, **ResourceId**, **Copyable** and **Url**\.
  + **LinkType** can be external or connect application such as case\.
    + When it is *external*, a user can navigate to a new browser page, which is configured with **Url**\.
    + When it is *case*, a user can navigate to a new case detail on the Agent workspace, which configured with ResourceId\.
  + **Copyable** allows users to copy the ResourceId by choosing it with your input device\.

**Graphic \(Optional\)**
+ Object with the following key:
  + Include \- boolean, if this is true then the graphic will be included in the page\.

**SubHeading \(Optional\)**
+ Secondary message for the page\.
+ Text only\.

**Input Data Example**

```
 {
  "AttributeBar": [
    { "Label": "Attribute1", "Value": "Value1" },
    { "Label": "Attribute2", "Value": "Value2" },
    { "Label": "Attribute3", "Value": "Amazon", "LinkType": "external", "Url": "https://www.amzon.com" }
  ],
  "Next": {
    "Label": "Go Home"
  },
  "Graphic": {
    "Include": true
  },
  "Heading": "I have updated your car rental reservation for pickup on July 22.",
  "SubHeading": "You will be receiving a confirmation shortly. Is there anything else I can help with today?",
}
```

**Output Data Example**

```
 {
    "Action": "Next",
    "Output": {
        "Label": "Go Home"
    }
}
```

**Input Data Schema**

```
                         {
  "AttributeBar": [
    {"Label": "Queue", "Value": "Sales"},
    {"Label": "Case ID", "Value": { "ExternalLink": {"Url": "https://...", "Label": "1234567"}}},
    {"Label": "Case", "Value": "New reservation"}
  ],
  "Graphic" {
    "Include": true
  },
  "Headline": "I have updated your car reservation ....",
  "SubHeadline": "You will be receiving a confirmation ...",
  "PrimaryPageNav: {
    "Label": "Back to Home"
  }
}
```

------
#### [ Cards view ]

The Cards view allows you to present a set of topics to your agent to choose from in order to dive deeper into a solution\. You can organize your topics as either entities \(e\.g\., products, reservations, orders\) that when clicked on reveal more info, or as the beginning of new workflows \(e\.g\., make a reservation\)\.

*Present cards to your agents\.*

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/solve-view-sq.png)

*When you choose a card, more info is revealed\.*

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/card-view-sq.png)

**Cards**
+ Required, must be provided to compose *Card* and *Detail*\.
+ Is a list of objects with *Card* and *Detail*\.
+ Card
  + *Title* is required and if provided, will display *Text* as the title of the card view\.
    + It should be a string\.
  + *Id* is optional, and if provided, will include the card information as part of output\.
    + It should be a string\. if it is not defined, we use index of the data\.
  + *Icon* is optional, and if provided, will display an icon at the left side of the title\.
    + It should be a name of the icon assets\.
  + *Status* is optional and if provided, will display a status at the top of the title\.
    + It should be a string\.
  + *Description* is optional and if provided, will display a description under the title\.
    + It should be a string\.
+ Detail
  + *Title* is required and if provided, will display Text as the tile of detail view\.
    + It should be a string\.
  + *Description* is optional, if provided, will display description text under the title\.
    + It should be a string\.
  + *Content* is optional and if provided will display the content provided\.
    + It can be either a string or TemplateString\.
  + *Actions* is optional and it can be strings or external actions\.
    + ExternalAction will open in a new tab\.

**AttributeBar \(Optional\)**
+ Optional, if provided will display the Attribute bar at the top of the view\.
+ Is a list of objects with required properties, **Label**, **Value**, and optional properties **LinkType**, **ResourceId**, **Copyable** and **Url**\.
  + **LinkType** can be external or connect application such as case\.
    + When it is *external*, a user can navigate to a new browser page, which is configured with **Url**\.
    + When it is *case*, a user can navigate to a new case detail on the Agent workspace, which configured with ResourceId\.
  + **Copyable** allows users to copy the ResourceId by choosing it with your input device\.

**Back \(Optional\)**
+ Optional, but required if no actions are included\. if provided will display the back navigation link\.
+ Is an object with a *Label* which will control what is displayed in the link text\.

**Title \(Optional\)**
+ Optional, if provided, will display the Text as the title with container shape

**NoMatchFound \(Optional\)**
+ Label, required if NoMatchFound is included\.
  + Overrides the default label of “It’s something else”\.

**Input Data Example**

```
{
    "AttributeBar": [{
            "Label": "Queue",
            "Value": "Sales"
        },
        {
            "Label": "Case ID",
            "Value": "1234567"
        },
        {
            "Label": "Case",
            "Value": "New reservation"
        },
        {
            "Label": "Attribute  3",
            "Value": "Attribute"
        }
    ],
    "Back": {
        "Label": "Back"
    },
    "Heading": "Customer may be contacting about...",
    "Cards": [{
              "Summary": {
                "Id": "lost_luggage",
                "Icon": "plus",
                "Heading": "Lost luggage claim"
              },
              "Detail": {
                "Heading": "Lost luggage claim",
                "Description": "Use this flow for customers that have lost their luggage and need to fill a claim in order to get reimbursement. This workflow usually takes 5-8 minutes",
                "Sections": {
                  "TemplateString": "<TextContent>Steps:<ol><li>Customer provides incident information</li><li>Customer provides receipts and agrees with amount</li><li>Customer receives reimbursement</li></ol></TextContent>"
                },
                "Actions": [
                  "Start a new claim",
                  "Something else"
                ]
              }
            },
            {
              "Summary": {
                "Id": "car_rental",
                "Icon": "Car Side View",
                "Heading": "Car rental - New York",
                "Status": "Upcoming Sept 17, 2022"
              },
              "Detail": {
                "Heading": "Car rental - New York",
                "Sections": {
                  "TemplateString": "<p>There is no additional information</p>"
                }
              }
            },
            {
              "Summary": {
                "Id": "trip_reservation",
                "Icon": "Suitcase",
                "Heading": "Trip to Mexico",
                "Status": "Upcoming Aug 15, 2022",
                "Description": "Flying from New York to Cancun, Mexico"
              },
              "Detail": {
                "Heading": "Trip to Mexico",
                "Sections": {
                  "TemplateString": "<p>There is no additional information</p>"
                }
              }
            },
            {
              "Summary": {
                "Id": "fligh_reservation",
                "Icon": "Airplane",
                "Heading": "Flight to France",
                "Status": "Upcoming Dec 5, 2022",
                "Description": "Flying from Miami to Paris, France"
              },
              "Detail": {
                "Heading": "Flight to France",
                "Sections": {
                  "TemplateString": "<p>There is no additional information</p>"
                }
              }
            },
            {
              "Summary": {
                "Id": "flight_refund",
                "Icon": "Wallet Closed",
                "Heading": "Refund flight to Atlanta",
                "Status": "Refunded July 10, 2022"
              },
              "Detail": {
                "Heading": "Refund trip to Atlanta",
                "Sections": {
                  "TemplateString": "<p>There is no additional information</p>"
                }
              }
            },
            {
              "Summary": {
                "Id": "book_experience",
                "Icon": "Hot Air Balloon",
                "Heading": "Book an experience",
                "Description": "Top experience for european travellers"
              },
              "Detail": {
                "Heading": "Book an experience",
                "Sections": {
                  "TemplateString": "<p>There is no additional information</p>"
                }
              }
            }],
    "NoMatchFound": {
        "Label": "Can't find match?"
    }

}
```

**Output Data Example**

```
{
    Action: "ActionSelected",
    Output: {
        actionName: "Update the trip"
    }
}
```

**Input Data Schema**

```
 {
    "AttributeBar": [
      {"Label": "Queue", "Value": "Sales"},
      {"Label": "Case ID", "Value": { "ExternalLink": {"Url": "https://...", "Label": "1234567"}}},
      {"Label": "Case", "Value": "New reservation"}
    ],
    "PrimaryPageNav": {
      "Label": "Back"
    },
    "Title": "José may be contating about...",
    "Cards": [
      {
        "Match": {
            "id" :"newReservation", 
            "Icon": "plus",
            "Title": "Make new reservation", 
        },
        "Solve": {
            "Title": "Make new reservation",
            "Description": "You can make a single reservation or include multiple items to get access to discounts.",
            "Content": {
              "TemplateString: "JSX string"
            },
            "Actions": ["Action 1", "Action 2", "Action 3", {"ExternalAction": {"Url": ...., "Label": "Go Somewhere"}}]  
        }
      },
      {
        "Match": {
            "id" :"rental", 
            "Icon": "Car Side View",
            "Title": "Car rental - New York",
            "Status": "Upcoming Sep 17, 2022",
            "Description": "Short optional description here."
        },
        "Solve": {...}
      },
      {
        "Match": {
            "id" :"upcoming", 
            "Icon": "Car Side View",
            "Title": "Car rental - New York",
            "Status": "Upcoming Sep 17, 2022",
            "Description": "Short optional description here."
        },
        "Solve": {...}
      }
    ],
    "NoMatchFound": {
      "Label": "It's Something Else"
    }
  }
```

------