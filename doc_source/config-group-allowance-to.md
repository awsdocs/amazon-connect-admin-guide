# Set group allowance<a name="config-group-allowance-to"></a>

Managers can set the maximum time off hours that agents combined can take within the Staffing Group for each calendar day for specific time off activities\.

For example, your business provides time off in December\. Here's how you might use the time off request feature:
+ Managers can allow a group of agents to take *casual leave* and *regular P\.T\.O* that add up to a maximum of 12 hours on December 20th and the 21st\.
+ They can automatically decline those types of time off requests on December 22nd and the 23rd by giving a value of `0` \- Zero hours\.
+ Adding value `0` allows them to specify blocked days\. Amazon Connect ignores a group allowance check if no value is specified\.

This allows the workforce managers to balance an agent’s personal time off needs with business headcount needs\. 

Managers can select the `+` sign to add multiple group allowance hours for different types of time off\. For example, a manager can allow 28 hours of health related time offs for November 23rd but only 8 hours of casual time off\.

The following image shows the calendar that would result for November 23, December 22 and 23\.

![\[The request management section, the option to enable time off request for this staffing group.\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/group-allowance-to.png)