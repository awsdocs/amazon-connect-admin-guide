# Schedule adherence usage examples<a name="schedule-adherence-usage-examples"></a>

**Shift activities that are tracked for adherence**

Any shift activity that is marked as `Adherence = Yes`\. If a shift is marked as `Adherence = No`, adherence is not calculated for that shift\. 

**How to determine which Agent State an agent should be in for each activity**

If an activity is marked as productive, an agent needs to be in an *Available* agent state\. Productivity is determined by the agent being in an available state and is not impacted if the agent isn’t handling live contacts\. For tracking how many contacts an agent has handled, see the occupancy metric\. 

If an activity is marked as non\-productive, an agent needs to be in a non\-productive custom state\. An agent does not have to be in a specific custom state to be considered adherent\. For example, if the shift activity is *Lunch*, but the agent switches their status to *Break*, the agent would still be considered adherent since both states are Non\-Productive\.

**What happens when\.\.\.**
+ **an agent starts working before their schedule starts**

  If an agent does not have a schedule, we do not track adherence for that time\. This means that if an agent starts working 5 minutes before or 5 minutes after their schedule, it will not count against their adherence\. However, if they decide to leave work 5 minutes early because they started 5 minutes early, they would be considered non\-adherent for that 5 minute interval\. 
+ **an agent flips to offline when they are supposed to be a non\-productive state**

  This would be considered non\-adherent because the agent state is offline, rather than Non\-Productive Time\. 
+ **an agent leaves training to answer contacts because of high contact volume**

  In this scenario, the agent would be marked as non\-adherent\. However, if leaving training is intended, you can adjust the schedule retroactively and adherence will be re\-calculated with the new shift\.
+ **a historical schedule is changed**

  If an agent’s schedule is changed within the last 30 days from the current date \(not the date of the schedule\), adherence will be re\-calculated with the new schedule\. This allows making real\-time adjustments to an agent's shift and will correctly evaluate their adherence\.