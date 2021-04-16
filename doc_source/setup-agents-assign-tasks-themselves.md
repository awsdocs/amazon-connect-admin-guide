# Set up agents to assign tasks to themselves<a name="setup-agents-assign-tasks-themselves"></a>

For an agent to be able receive a task, they need a quick connect created for them\. With this quick connect, agents will be able to assign tasks to themselves, and other agents will be able to assign tasks to them\. 

## Step 1: Create a quick connect for the agent<a name="create-quick-connect-for-agent"></a>

1. On the navigation menu, choose **Routing**, **Quick connects**, **Add a new**\.

1. Enter a name for the quick connect, such as the name of the agent\. For example, if you want Jane Doe to be able to assign tasks to herself, enter **Jane Doe**\.

1. Under **Type**, use the dropdown list to choose **Agent**\.

1. Under **Destination**, use the dropdown list to choose the user name for the agent\.

1. Under **Contact flow**, choose **Default agent transfer**, or the appropriate contact flow for your contact center\.

1. Under **Description**, enter a description, such as **Jane Doe's quick connect**\.

1. Choose **Save**\.  
![\[Image NOT FOUND\]](http://docs.aws.amazon.com/connect/latest/adminguide/images/tasks-agent-quick-connect.png)

## Step 2: Create a queue for the agent and associate the quick connect<a name="create-queue-for-agent"></a>

1. After you create the quick connect, go to **Routing**, **Queues** and add a queue for the agent\. 

1. On the **Add new queue** page, in the **Quick connects** box, search for the quick connect you created for the agent\. 

1. Select the quick connect and then choose **Save**\.

## Step 3: Add the queue to the agent's routing profile<a name="add-queue-to-agent-profile"></a>

1. Go to **Users**, **Routing profiles** and choose the agent's routing profile\. 

1. Add the agent's queue to the routing profile, and choose **Task** for the channel\.

   If the agent can receive transfers through other channels, select them as well\.

1. Choose **Save**\.