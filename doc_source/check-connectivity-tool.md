# Use the Endpoint Test Utility<a name="check-connectivity-tool"></a>

To validate connectivity to Amazon Connect, or when your agents are experiencing problems with the Contact Control Panel \(CCP\), we recommend using the [Amazon Connect Endpoint Test Utility](https://www.connect-tools.net/endpoint-test/)\. 

The Amazon Connect Endpoint Test Utility performs the following checks: 
+ Validates that the browser being used supports WebRTC\.
+ Determines if the browser has appropriate access to media devices \(microphone, speakers, etc\)\.
+ Performs latency tests for all active Amazon Connect Regions\.
+ Performs latency tests to a specific Amazon Connect instance, if provided\.
+ Validates network connectivity across required ports for media streams\.

The complete results are available for download as a JSON file\. You can copy the results to include in a support ticket\. You can also load the results file into the tool by selecting the **Load previous results** option\. This option displays the contents of the file visually and makes it easier to analyze the results\. Additionally, you can download a bookmark specifically for the provided instance to make future tests easier to run\. 

## Parameters to customize the Endpoint Test Utility<a name="customize-check-connectivity-tool"></a>

Use the following URL parameters to customize the Endpoint Test Utility:
+ **lng**: Change the language of the tool\. Currently supported languages are English \(default\), Spanish, and French\. It accepts the following values:
  + en
  + es
  + fr
+ **autoRun**: Run the tool automatically\. It accepts the following values:
  + true
  + false
+ **connectInstanceUrl**: Specify the Amazon Connect instance in the URL\. It must start with **https**\.

Example customized URL:

`https://a.co/4pBJMng?lng=es&autoRun=true&connectInstanceUrl=https://myinstance.awsapps.com/connect/login` 

## Previous Check Connectivity Tool<a name="previous-check-connectivity-tool"></a>

The previous version of the tool is available here: [Amazon Connect Check Connectivity Tool](https://s3.amazonaws.com/connectivitytest/checkConnectivity.html)\. 

This tool checks which web browser the agent is running, and whether the microphone has required permissions\. Click the **Test** buttons to check the ports and latency\. 