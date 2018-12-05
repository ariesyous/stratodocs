# Topics

A topic is a list of people who will be notified when an alarm condition occurs on an instance.

**How to use a topic**

For example, you might want to create a topic called "Too much memory used on MyInstance." That topic would list the people who want to be notified when there is too much memory being used on MyInstance.

You would then  [create an alarm](https://www.stratoscale.com/knowledge/alarms)  that monitors how much memory is being used on MyInstance. When that alarm indicates that too much memory is being used, the system sends an email to all the people in the topic associated with that alarm, telling them about the excess memory usage.

**To create a topic**:

1. Click  **Menu**  >  **Region Monitoring**  >  **Topics**  >  **Create**.

**Name**: Type in the name of the topic you want to create, for example, "Too much memory usage on MyInstance"

**Emails**: Type in the email addresses of the people who should be alerted to the alarm conditions associated with this topic.

# Tasks

Tasks are asynchoronous processes running in the background of what is being implemented on the Symphony UI.

Click on the  **Tasks**  option on the Main Navigation pane.

The  **Tasks**  view appears.

![](https://www.stratoscale.com/wp-content/uploads/Tasks_1_Tasks20view.jpg)

The  **Tasks**  view lists all of the tasks that have been triggered on your system together with their Start and End times, the User and Project affiliated with the task, and the status of the task.

Tasks have four possible statuses:

-   In Progress
-   Finished
-   Failed
-   Queued

Symphony currently monitors two types of tasks:

-   Triggering of a Data Protection Plan (whether triggered manually or via scheduling)
-   The migrating of an Appliance after being uploaded