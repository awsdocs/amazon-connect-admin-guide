# Enable auto\-accept call for agents<a name="enable-auto-accept"></a>

When Auto\-Accept Call is enabled for an available agent, the agent connects to contacts automatically\. 

**How long until the call is connected to the agent?** Less than one second\. When a call arrives to an available agent who has Auto\-Accept Call enabled, the Contact Control Panel \(CCP\) briefly shows the options **Accept** or **Reject**\. This is expected behavior\. After less than a second, the call is automatically accepted and these options disappear\.

Auto\-Accept Call doesn't work for callbacks\.

You can't enable Auto\-Accept Call while editing multiple existing users in your Amazon Connect instance\. You must edit existing users individually to enable it\. You can also configure the setting for multiple new users when you bulk upload new users with the CSV template\. 

## Enable auto\-accept call for existing agents<a name="w58aac23c23c13c11"></a>

To complete these steps, you must log in as a user who has the following permissions in their security profile: **Edit, Create, Remove, Enable / Disable, and Edit permission**\.

1. Log in to your Amazon Connect instance using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. In the left navigation bar, choose **Users**, **User management**\.

1. In the list of users, select an agent, and then choose **Edit**\.

1. On the Edit users page, under Phone Type, select the **Auto\-Accept Call** check box\.

1. Choose **Save**\.

1. Repeat these steps for each user that you want to edit\.

## Bulk upload new users with auto\-accept call enabled<a name="bulk-upload-users-auto-accept"></a>

You can't use the CSV template to edit information for existing users\. If you include duplicate users with different information in the CSV template, you will receive an error\.

1. Log in to your Amazon Connect instance using your access URL \(https://*domain*\.awsapps\.com/connect/login\)\.

1. In the left navigation bar, choose **Users**, **User management**\.

1. Choose **Add new users**\.

1. Under **How do you want to set up your existing users?**, next to **Upload my users from a template \(csv\)**, choose **template** to download a pre\-formatted CSV file\.

1. In the CSV file, configure the details for the new users who you want to add\. For **soft phone auto accept \(yes/no\)**, be sure to enter **yes**\.

1. After configuring the CSV file, in your Amazon Connect instance, choose **Upload my users from a template \(csv\)**, and then choose **Next**\.

1. Under **Select and upload a spreadsheet with user details**, choose **Choose file**\.

1. Choose the configured CSV file from its location on your computer\.

1. In your Amazon Connect instance, choose **Upload and verify**\.

1. Under **Verify user details**, verify that the information is correct for the new users, and then choose **Create users**\.

## \(Optional\) Verify the change in CCP logs<a name="bulk-upload-users-auto-accept-verify"></a>

To confirm that **Auto\-Accept Call** is enabled for an agent, download the CCP logs generated for that agent: in the CCP for the agent, choose **Settings**, **Download logs**\. The logs are saved to your browser's default download directory\. 

In the logs, the **autoAccept** attribute is set to **"true"** if this setting is enabled\. The logs show something like this:

```
                  "type": "agent",
                  "initial": false,
                  "softphoneMediaInfo": {
                       "callType": "audio_only",
                       "autoAccept": true
```