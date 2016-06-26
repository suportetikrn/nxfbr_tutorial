GUI - Dashboard, Logging, Report
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
NxFilter keeps its log data up to 400 days and you can generate a daily, weekly, per-user report based on the log data.
Main
When you login to your admin GUI you will see the dashboard of NxFilter. There are several charts for showing a summary for the last 2 hours. On the bottom of the dashboard you can see 10 recent block logs for the last 12 hours.
* The difference between 'request-sum' and 'request-cnt' is from NxFilter's logging system. To reduce the amount of disk access NxFilter keeps all the log data into its memory space. And then it flushes the data once a minute. If there is a request for the same domain from the same user in a minute it only increases the count for the data. So 'request-sum' means the sum of all the counts and 'request-cnt' means the count for all the unique data.
Logging
You can search user request log with various conditions in 'Logging > Request'. Logging data is being updated once in a minute to reduce the load on DB.
In 'Logging > Signal' you can view the log of the signals from the agents of NxFilter.
In 'Logging > NetFlow' you can monitor NetFlow data imported.
* Use square brackets for the exact matching keyword on log search.
    ex) [nxfilter], [192.168.0.100]
Report
NxFilter generates a daily, weekly, per-user report.
