# Symphony-supported AWS – Cloudwatch APIs and Parameters

Below is a list of the AWS - Cloudwatch APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

<table>
<thead>
<tr class="header">
<th>Name</th>
<th>Required Parameters</th>
<th>Optional Parameters</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_DeleteAlarms.html" class="external-link">DeleteAlarms</a></td>
<td><ul>
<li>AlarmNames</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_DescribeAlarmHistory.html" class="external-link">DescribeAlarmHistory</a></td>
<td></td>
<td><ul>
<li>AlarmName</li>
<li>EndDate</li>
<li>HistoryItemType</li>
<li>MaxRecords</li>
<li>NextToken</li>
<li>StartDate</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_DescribeAlarms.html" class="external-link">DescribeAlarms</a></td>
<td></td>
<td><ul>
<li>ActionPrefix</li>
<li>AlarmNamePrefix</li>
<li>AlarmNames</li>
<li>MaxRecords</li>
<li>NextToken</li>
<li>StateValue</li>
</ul></td>
</tr>
<tr class="even">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_DisableAlarmActions.html" class="external-link">DisableAlarmActions</a></td>
<td><ul>
<li>AlarmNames</li>
</ul></td>
<td></td>
</tr>
<tr class="odd">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_EnableAlarmActions.html" class="external-link">EnableAlarmActions</a></td>
<td><ul>
<li>AlarmNames</li>
</ul></td>
<td></td>
</tr>
<tr class="even">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_PutMetricAlarm.html" class="external-link">PutMetricAlarm</a></td>
<td><ul>
<li>AlarmName</li>
<li>ComparisonOperator</li>
<li>EvaluationPeriods</li>
<li>MetricName</li>
<li>Namespace</li>
<li>Period</li>
<li>Threshold</li>
</ul></td>
<td><ul>
<li>ActionsEnabled</li>
<li>AlarmActions</li>
<li>AlarmDescription</li>
<li>DatapointsToAlarm</li>
<li>Dimensions</li>
<li>EvaluateLowSampleCountPercentile</li>
<li>ExtendedStatistic</li>
<li>InsufficientDataActions</li>
<li>OKActions</li>
<li>Statistic</li>
<li>TreatMissingData</li>
<li>Unit</li>
</ul></td>
</tr>
<tr class="odd">
<td><a href="https://docs.aws.amazon.com/AmazonCloudWatch/latest/APIReference/API_SetAlarmState.html" class="external-link">SetAlarmState</a></td>
<td><ul>
<li>AlarmName</li>
<li>StateReason</li>
<li>StateValue</li>
</ul></td>
<td><ul>
<li>StateReasonData</li>
</ul></td>
</tr>
</tbody>
</table>