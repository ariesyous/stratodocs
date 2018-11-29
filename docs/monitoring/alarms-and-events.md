# Alarms and Events Overview

Symphony monitors conditions and actions that occur in your system.

Alarms are notifications about conditions in the system which threaten the integrity of the system. For example, an alarm can be triggered once an internal service is down, or when a connectivity between two nodes is lost. By definition, an alarm requires human intervention to remove the system-threatening conditions.

Events are notifications about any actual changes or attempts at changes in the state of Symphony, whether initiated manually or automatically by the system. Symphony provides you with information about their occurrences in the form of events. The monitored actions include actions that were prompted by the user, such as the creation and stopping of a VM, and activities and processes that occur in the system without direct intervention, such as a disk failure and a high CPU utilization.

Each event has a severity level. Symphony includes a set of pre-defined events and alarms.

The events and alarms appear in Symphony in three different places

-   In the  **System Overview**  view there are Alarms and Events widgets each displaying the number of Alarms or Events per type of Alarm or Event.
-   In the  **Alarms & Events**  view there are lists of Alarms and Events with detailed information about each.
-   In addition, they appear in the context of the entity to which they refer. For example, Alarms or Events that are related to a certain node will appear in the  **NODE**  view of this specific node. Currently, Alarms and Events appear in the context of specific  **Nodes, Disks or VMs**.