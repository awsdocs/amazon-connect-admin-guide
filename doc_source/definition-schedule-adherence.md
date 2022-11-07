# Historical Schedule Adherence<a name="definition-schedule-adherence"></a>

This section describes the values used when calculating Historical Schedule Adherence\.

**Adherence**

Percentage of time that an agent correctly follows their schedule\. This is measured by tracking if an agent is in an *Available* agent status when they should be in productive state\. This percentage is calculated as follows:

Adherence % = \(\(Total Adherent Minutes\)/ Total Scheduled Adherence Minutes\)

An agent is considered adherent if the agent is in an *Available* Status, when the shift activity is Productive, or if the agent is in Non\-Productive Status \(i\.e Custom Status\), when the shift activity is Non\-Productive\. Otherwise the agent is considered non\-adherent\. This means that if a shift activity is called *Lunch* but marked as productive, the agent is considered adherent if they are in the *Available* agent status\. 
+ Type: String
+ Min value: 0\.00%
+ Max value: 100\.00%
+ Category: Agent activity\-driven metric

**Note**  
Anytime you change the schedule, Schedule Adherence is re\-calculated up to 30 days in the past from the current date \(not the date of the schedule\), if schedules are changed\.

**Adherent time**

Total time an agent was in an *Available* status when their shift activity is productive or was is in non\-productive status when the shift activity is non\-productive\.
+ Type: String \(hh:mm:ss\)
+ Category: Agent activity\-driven metric

**Non\-Adherent time**

Total time an agent was not in an *Available* status when their shift activity is productive or not in a non\-productive status when their shift activity is non\-productive\.
+ Type: String \(hh:mm:ss\)
+ Category: Agent activity\-driven metric

**Scheduled time**

Total time an agent was scheduled \(either for productive or non\-productive time\) and Adherence for those shifts were set to `Yes`\. 
+ Type: String \(hh:mm:ss\)
+ Category: Agent activity\-driven metric