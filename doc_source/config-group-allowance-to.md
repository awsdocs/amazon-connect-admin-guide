# Configure group allowance<a name="config-group-allowance-to"></a>

**Set group allowance**

Managers can set the maximum time off hours that agents combined can take within the Staffing Group for each calendar day for specific time off activities\.

For example, if your business provides time off in December, managers can allow a group of agents to take time offs of type *casual leave* and *regular P\.T\.O* that add up to a maximum of 12 hours on December 20th and the 21st but can automatically decline those types of time off requests on December 22nd and the 23rd by giving a value of `0` \- Zero hours\. Adding value `0` allows them to specify blocked days\. The system would ignore a group allowance check if no value is specified\. This allows the workforce managers to balance an agent’s personal time off needs with business headcount needs\. Managers can select the `+` sign to add multiple group allowance hours for different types of time off\. This means that a manager can allow 28 hours of health related time offs for November 23rd but only 8 hours of casual time off\.

![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/group-allowance-to.png)