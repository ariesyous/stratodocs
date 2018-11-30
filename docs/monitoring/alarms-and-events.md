# Alarms and Events Overview

Symphony monitors conditions and actions that occur in your system.

Alarms are notifications about conditions in the system which threaten the integrity of the system. For example, an alarm can be triggered once an internal service is down, or when a connectivity between two nodes is lost. By definition, an alarm requires human intervention to remove the system-threatening conditions.

Events are notifications about any actual changes or attempts at changes in the state of Symphony, whether initiated manually or automatically by the system. Symphony provides you with information about their occurrences in the form of events. The monitored actions include actions that were prompted by the user, such as the creation and stopping of a VM, and activities and processes that occur in the system without direct intervention, such as a disk failure and a high CPU utilization.

Each event has a severity level. Symphony includes a set of pre-defined events and alarms.

The events and alarms appear in Symphony in three different places

-   In the  **System Overview**  view there are Alarms and Events widgets each displaying the number of Alarms or Events per type of Alarm or Event.
-   In the  **Alarms & Events**  view there are lists of Alarms and Events with detailed information about each.
-   In addition, they appear in the context of the entity to which they refer. For example, Alarms or Events that are related to a certain node will appear in the  **NODE**  view of this specific node. Currently, Alarms and Events appear in the context of specific  **Nodes, Disks or VMs**.

# Creating Alarms

You can create alarms that notify you of various system conditions on instances in your Symphony region. For example, you can create an alarm that tells you when a certain instance has memory usage over a specified GB threshold.

Once you create an alarm, it appears in Region Monitoring alarms list with its state displayed (ALARM, OK, INSUFFICIENT DATA). You can also set notifications on the alarm, so that when the alarm goes off, it sends an email to a list of watchers.

**To create an alarm**:

1. Click  **Menu**  >  **Region Monitoring**  >  **Alarms**  >  **Create**.

2. Fill in the following fields, then click  **Finish**.

<table class="wrapped confluenceTable"><colgroup><col style="width: 127.0px;"><col style="width: 1068.0px;"></colgroup><tbody><tr><th colspan="2" style="text-align: center;" class="confluenceTh">Alarm</th></tr><tr><td class="confluenceTd"><strong>Field</strong></td><td class="confluenceTd"><strong>Description</strong></td></tr><tr><td class="confluenceTd">Name</td><td class="confluenceTd">Name you want to give the alarm.</td></tr><tr><td class="confluenceTd">Description</td><td class="confluenceTd">Optional description.</td></tr><tr><td colspan="2" style="text-align: center;" class="confluenceTd"><em>Trigger Conditions</em></td></tr><tr><td class="confluenceTd">Instance</td><td class="confluenceTd">Select the instance you want to set the alarm for.</td></tr><tr><td class="confluenceTd">Statistic</td><td class="confluenceTd"><p>Select one of the following:</p><p>Average</p><p>Sum</p><p>Minimum</p><p>Maximum</p></td></tr><tr><td class="confluenceTd">Metric</td><td class="confluenceTd"><p>Select one of the following:</p><p>CPUUsed</p><p>CPUUtilization</p><p>MemoryUsed</p><p>MemoryUtilization</p><p>NetworkIn</p><p>NetworkOut</p></td></tr><tr><td class="confluenceTd">Threshold</td><td class="confluenceTd"><p>In the Threshold drop down, select one of these operators:</p><p>&gt;=</p><p>&gt;</p><p>&lt;</p><p>&lt;=</p></td></tr><tr><td class="confluenceTd">Than</td><td class="confluenceTd"><p>In the Than drop down, select an integer that corresponds to the appropriate unit of measurement for the metric.&nbsp;The system automatically notes which metric you select, and then displays an appropriate measurement unit for that metric.</p><p>For example, if you are measuring MemoryUsed, the unit of measurement in the Than drop down would be GB.</p><p><strong>Final statement = Combination of Metric, Threshold, and Than fields</strong>: Continuing with this example, the final statement (combining Metric, Threshold, and Than fields) might read:</p><p>MemoryUsed &gt;= 3GB</p></td></tr><tr><td class="highlight-grey confluenceTd" colspan="2" data-highlight-colour="grey" style="text-align: center;"><strong>Notifications</strong></td></tr><tr><td colspan="2" class="confluenceTd"><p>You can optionally have an alarm send emails to a list of people, letting them know when the alarm is in various states. For example, you can set things up so that people are notified if the alarm is triggered (is in the active state).</p><p>Alarm states are listed in the alarms list in the GUI: <strong>Menu</strong> &gt; <strong>Region Monitoring</strong> &gt; <strong>Alarms</strong> &gt; <strong>State</strong> field. Possible states are ALARM, OK, INSUFFICIENT DATA.</p><p>Before using this feature, you need to group your list of email addresses (people who are watching an alarm) into <a href="https://www.stratoscale.com/knowledge/topics"><span class="confluence-link">topics</span></a>. You can then specify a topic for the following alarm conditions:</p></td></tr><tr><td colspan="1" class="confluenceTd">On alarm active</td><td colspan="1" class="confluenceTd"><p>Notify topic watchers when the alarm state is ALARM (alarm has been triggered).</p><p>Select the topic whose watchers you want to notify.</p></td></tr><tr><td colspan="1" class="confluenceTd">On alarm off</td><td colspan="1" class="confluenceTd"><p>Notify topic watchers when the alarm state moves from ALARM to OK (alarm conditions are no longer met).</p><p>Select the topic whose watchers you want to notify.</p></td></tr><tr><td colspan="1" class="confluenceTd">On insufficient data</td><td colspan="1" class="confluenceTd"><p>Notify topic watchers when the alarm state is INSUFFICIENT DATA.</p><p>Select the topic whose watchers you want to notify.</p></td></tr></tbody></table>


# Events

Events are any actual changes or attempts at changes in the state of Symphony, whether initiated manually or automatically by the system.

To display events, from the Main Navigation pane, click  **Alarms & Events**  >  **Events**.

The  **Events**  view appears, listing all of the events that have occurred in your system.

**Related Topics**

[Sorting and filtering events](https://www.stratoscale.com/knowledge/region-monitoring/alarms-and-events/events/#Events-Sort)

For each event the following information is provided:

-   **Severity**– the severity level of the event:
    -   **Info**  – Normal operational messages that require no action.
    -   **Warning**  - This may indicate that an error will occur if you do not take action.
    -   **Error**  – You should carefully review events with this severity level.
-   **Time**  – The date and time that the event occurred.
-   **Entity Type**  - The type of entity that this event pertains to. Entity Type can include values such as:
    
    disk
    
    image
    
    network
    
    nic
    
    node
    
    pool
    
    project
    
    service
    
    snapshot
    
    subnet
    
    tenant
    
    user
    
    vm
    
    volume
    
-   **Name**  - Name of the event.
-   **Details**  - Additional details about the event.
-   **Project**  - The project in whose context the event took place. If an event was performed in the context of the entire cluster this field will remain empty.

Events are stored in the  **Events**  widget for a month. Even if the state that is reported in the event has changed, the event will still be displayed in the Events widget.

## Sorting and filtering events

You can  **sort**  events by clicking each column heading. For example, to sort by severity, click the Severity heading.

You can  **filter**  events by date, severity, and search terms:

![](https://www.stratoscale.com/wp-content/uploads/events_filter.png)

**Date and time**. To filter by date and time, click inside the date box. This displays the calendar window. Click on the calendar entries for the start date and the end date. If you want to specify a particular hour and minute on each day, click  **Select Time**, set the times, then click  **OK**.

**Severity filters: Error, Warning, Info**. To display only events that have a certain severity, click the pre-set filters for Error, Warning, or Info. For example, to display only errors, click Error.

**Filter search box**. You can search for any term that appears in an event. In addition, you can search for events that have a column entry set to a specific value, using this syntax:

_column_header:value_

For example, to search for events that have their Entity Type column entry set to vm, use this syntax:

entity_type:vm

**Removing filters**. To remove all filters/searches, click  **Reset All**.

