# Add interactive messages to chat<a name="interactive-messages"></a>

Interactive messages are rich messages that present a prompt and pre\-configured display options that a customer can select from\. These messages are powered by Amazon Lex and configured through Amazon Lex using a Lambda\. 

**Tip**  
For step\-by\-step instructions on how to add interactive messages through Amazon Lex and Lambda, see this blog: [Set up interactive messages for your Amazon Connect chatbot](https://aws.amazon.com/blogs/contact-center/easily-set-up-interactive-messages-for-your-amazon-connect-chatbot/)\.

Amazon Connect provides two message display templates: a list picker and a time picker\. These templates define how the information is going to render, and what information is surfaced in the chat interface\. When interactive messages are sent through chat, contact flows validate that the message format follows one of these templates\.

This topic provides details about these interactive message templates\.

## List picker template<a name="list-picker"></a>

Following are examples of how the list picker template renders information in a chat\. 

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/interactive-messages-listpicker-images2.png)

The following code is the list picker template that you can use in your Lambda\. Note the following:
+ **Bold text** is a mandatory parameter\.
+ In some cases, if the parent element exists in the request and it isn't mandatory/bold, but the fields in it are, then the fields are mandatory\. For example, see `data.replyMessage` structure in the following template\. If the structure exists, title is mandatory\. Otherwise complete `replyMessage` is optional\. 

**Important**  
Images should be uploaded in Amazon S3 and publicly accessible\.

```
{
   "templateType":"ListPicker",                       (mandatory)
   "version":"1.0",                                   (mandatory)
   "data":{                                           (mandatory)
      "replyMessage":{                             
         "title":"Thanks for selecting!",             (mandatory)
         "subtitle":"Produce selected",
         "imageType":"URL",                                
         "imageData":"https://interactive-msg.s3-us-west-2.amazonaws.com/fruit_34.3kb.jpg",                          
         "imageDescription":"Select a produce to buy"
      },
      "content":{                                        (mandatory)
         *"title":"What produce would you like to buy?", (mandatory)
         "subtitle":"Tap to select option",
         "imageType":"URL",                       
         "imageData":"https://interactive-msg.s3-us-west-2.amazonaws.com/fruit_34.3kb.jpg",                  
         "imageDescription":"Select a produce to buy",
         "elements":[                                   (mandatory, 1-6 items)
            {
               "title":"Apple",                          (mandatory)
               "subtitle":"$1.00"
               "imageType":"URL",
               "imageData":"https://interactive-message-testing.s3-us-west-2.amazonaws.com/apple_4.2kb.jpg"
            },
            {
               "title":"Orange",                         (mandatory)
               "subtitle":"$1.50"
               "imageType":"URL",                  
               "imageData":"https://interactive-message-testing.s3-us-west-2.amazonaws.com/orange_17.7kb.jpg",           
            },
             {
               "title":"Banana",                         (mandatory)
               "subtitle":"$10.00"
               "imageType":"URL",                  
               "imageData":"https://interactive-message-testing.s3-us-west-2.amazonaws.com/banana_7.9kb.jpg",            
               "imageDescription":"Banana"
            }
         ]
      }
   }
}
```

### List picker limits<a name="list-picker-limits"></a>

The following table lists the limits for each of the list picker elements, should you choose to build your own Lambda from scratch\. The mandatory parameters are in bold\.


****  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/interactive-messages.html)

## Time picker template<a name="list-picker-images"></a>

Following are two examples of how the time picker template renders information in a chat\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/interactive-messages-timepicker.png)

The following code is the time picker template that you can use in your Lambda\.  Note the following:
+ **Bold text** is a mandatory parameter\.
+ In some cases, if the parent element exists in the request and it isn't mandatory/bold, but the fields in it are, then the fields are mandatory\. For example, see `data.replyMessage` structure in the following template\. If the structure exists, title is mandatory\. Otherwise complete `replyMessage` is optional\. 

```
{
   "templateType":"TimePicker",                                 (mandatory)
   "version":"1.0",                                             (mandatory)
   "data":{                                                     (mandatory)
      "replyMessage":{
         "title":"Thanks for selecting",                        (mandatory)
         "subtitle":"Appointment selected",
      },
      "content":{                                               (mandatory)
         "title":"Schedule appointment",                        (mandatory)
         "subtitle":"Tap to select option",
         "timeZoneOffset":-450
         "location":{
            "latitude":47.616299,                               (mandatory)
            "longitude":-122.4311,                              (mandatory)
            "title":"Oscar"                                     (mandatory)
            "radius":1,
         },
         "timeslots":[                                          (mandatory, 1-20 items)
               {
                  "date" : "2020-10-31T17:00+00:00"             (mandatory)
                  "duration": 60,                               (mandatory)
               },
               {
                  "date" : "2020-11-15T13:00+00:00"            (mandatory)
                  "duration": 60,                              (mandatory)
               },
               {
                  "date" : "2020-11-15T16:00+00:00"            (mandatory)
                  "duration": 60,                              (mandatory)
               }
            ],           
         }
      }
   }
}
```

### Time picker limits<a name="time-picker-limits"></a>

The following table lists the limits for each of the time picker elements\. Use this information if you choose to build your own Lambda from scratch\. The mandatory parameters are in bold\.


****  
[\[See the AWS documentation website for more details\]](http://docs.aws.amazon.com/connect/latest/adminguide/interactive-messages.html)