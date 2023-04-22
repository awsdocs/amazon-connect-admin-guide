# Investigate common issues with adding a chat user interface to your website<a name="ts-cw"></a>

This topic is for developers who need to investigate issues that may occur when configuring a chat widget in the Amazon Connect console\. 

If you see the following **Something went wrong** error message when loading your chat widget, open the browser tools to view the error logs\. 

![\[An error message that says Something went wrong.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/chatwidget-error-message.png)

Following are common issues that cause this error\.

## 400 Invalid request<a name="400-invalid-request"></a>

If the logs mention a 400 invalid request, there are a few possible causes:
+ Your chat widget is not being served on an allowed domain\. You must specifically state the domains where you will host your widget\.
+ The request to the endpoint is not properly formatted\. This usually occurs only if the contents of the embed snippet have been modified\.

## 401 Unauthorized<a name="401-unauthorized"></a>

If the logs mention a 401 unauthorized, this is a problem with the JSON Web Token \(JWT\) authentication\. 

After you have the JWT, you need to implement it in the `authenticate` callback function\. The following example shows how to implement it if you're trying to fetch your token and then use it: 

```
amazon_connect('authenticate', function(callback) {
  window.fetch('/token').then(res => {
    res.json().then(data => {
      callback(data.data);
    });
  });
});
```

Here is a more basic version of what needs to be implemented:

```
amazon_connect('authenticate', function(callback) {
   callback(token);
});
```

For instructions on implementing JWT, see [Step 3: Confirm and copy chat widget code and security keys](add-chat-to-website.md#confirm-and-copy-chat-widget-script)\.

If you have implemented the callback already, the following scenarios may still cause a 401:
+ Invalid signature
+ Expired token

## 404 Not found<a name="404-not-found"></a>

A 404 status code indicates that your `widgetId` cannot be found\. Verify that your snippet is exactly how it was copied from the Amazon Connect website, and none of the identifiers have changed\.

If the identifiers have not changed and you are seeing a 404, contact AWS Support\. 

## 500 Internal server error<a name="500-internalservererror-chatwidget"></a>

This can be caused by your service\-linked role not having the required permissions to start chat\. This happens if your Amazon Connect instance was created before October 2018 because you don’t have service\-linked roles set up\.

**Solution**: Add the `connect:*` policy on the role that is associated with your Amazon Connect instance\. For more information, see [Use service\-linked roles for Amazon Connect](connect-slr.md)\.

If your service\-linked role has the correct permissions, contact AWS Support\.