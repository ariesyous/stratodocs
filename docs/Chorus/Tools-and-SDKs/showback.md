# Showback

Showback is the tool for displaying the usage of the virtual resources in your Symphony cluster. This usage serves as the basis for the charges for these resources

1.  ### Running showback from **inside Symphony Cluster**:
    

1.  1.  Connect to one of the nodes
    2.  To display the [usage and arguments](https://www.stratoscale.com/knowledge/tools-and-sdks/showback/#Showback-UsageandArguments) of the showback tool, run either
        
        [root@stratonode1 ~] # _showback -h_
        
        or
        
        [root@stratonode1 ~] # _showback --help_
        
    3.  Here is an example of how to use 'showback' to retrieve the metrics of the last 100 hours:
        
        [root@stratonode1 ~] # _showback --url https://virtual-nb.service.strato/ --insecure --domain cloud_admin --username admin --password admin --start_hours_ago 100_
        
        _--url_ - points to the virtual northbound address  
        _--insecure_ - is needed when using a non-secure connection  
        _--domain_ - is the account name (for example 'cloud_admin')  
        _--user_ - is the user in that account (for example 'admin')  
        _--password_ - is the password of that user
        
    4.  The output will be in table format which is human readable, but cannot be input as such, into a billing system.
        
    5.  For json or yaml output which can be used by a billing system, just add
        
        _--format json_
        
        _or_
        
        __--format yaml__
        
        to the command, as follows:
        
        [root@stratonode1 ~] # _showback --url https://virtual-nb.service.strato/ --insecure --domain cloud_admin --username admin --password admin --start_hours_ago 100 **--format json**_
        
2.  Running showback from a **Remote Server**:
    

1.  1.  Verify that you have a CentOS or Fedora installed on a VM or physical machine.
    2.  [Install the Symphony_client](https://www.stratoscale.com/knowledge/install-symphony-client-on-external-machine)  
        
    3.  Copy the showback.py script from
        
        _/usr/bin/showback_
        
        to the remote server.
        
    4.  Run the following command:
        
        _PYTHONPATH=/opt/symphony-client python showback.py --url [https://<](https://demo2.stratoscale.com/)cluster_IP> --insecure --domain cloud_admin --username admin --password admin --start_hours_ago 100 --format json_
        
        -   _PYTHONPATH=/opt/symphony-client -_ points you to the Symphony client
        -   _--url_ - points to the cluster IP

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-grey confluenceTd" colspan="2" data-highlight-colour="grey"><div class="content-wrapper"><p><strong><span class="confluence-anchor-link conf-macro output-inline" data-hasbody="false" data-macro-name="anchor" id="Showback-UsageandArguments"> </span>Usage</strong></p><p style="margin-left: 60.0px;">showback [-h] [--url URL [--domain DOMAIN] [--username USERNAME]</p><p style="margin-left: 120.0px;">[--password PASSWORD] [--tenant TENANT] [--format {table,json,yaml}]</p><p style="margin-left: 120.0px;">[--end_time END_TIME] [--insecure | --cert_file CERT_FILE]</p><p style="margin-left: 120.0px;">(--start_time START_TIME | --start_hours_ago START_HOURS_AGO)</p></div></td></tr><tr><td colspan="2" class="confluenceTd"><p><strong>Returns</strong></p><p style="margin-left: 60.0px;">Usage times of the system services</p></td></tr><tr><td class="highlight-grey confluenceTd" data-highlight-colour="grey"><strong>Optional Arguments</strong></td><td class="highlight-grey confluenceTd" data-highlight-colour="grey"><strong>Description</strong></td></tr><tr><td class="confluenceTd"><p>&nbsp;<span style="color: rgb(84,88,90);">-h, --help</span></p><p>--url URL</p><p>--domain DOMAIN</p><p>--username USERNAME</p><p>--password PASSWORD</p><p>--tenant TENANT</p><p>--format {table,json,yaml}</p><p>--end_time END_TIME</p><p>--insecure</p><p><span style="color: rgb(84,88,90);">--cert_file CERT_FILE</span></p><p>--start_hours_ago START_HOURS_AGO</p><p>--start_time START_TIME</p></td><td class="confluenceTd"><div class="content-wrapper"><p><span style="color: rgb(84,88,90);">Shows this help message and exits</span></p><p>URL of cluster from which to access data. e.g. http://10.11.12.13</p><p>Domain of user used to retrieve date</p><p>User name used to retrieve date</p><p>Password used to retrieve date</p><p>ID of tenant from which showback data is being retrieved</p><p>Output format of showback data. Default: table. (To truncate, rather than wrap, long table rows, add: '| less -S')</p><p>Time at which to to end showback, Format 'Y-m-d H:M:S'. E.g., '2017-06-05 09:07:06' Default: Current time</p><p>Do not verify SSL certificate. Default: SSL certificate-less verification</p><p><span style="color: rgb(84,88,90);">Full path to certificate file</span></p><p>Hours ago from END_TIME at which to start showback.</p><p>Time from which to start collecting showback data. Format 'Y-m-d H:M:S'. E.g., '2017-06-05 09:07:06'</p><div class="confluence-information-macro confluence-information-macro-note conf-macro output-block" data-hasbody="true" data-macro-name="note"><span class="aui-icon aui-icon-small aui-iconfont-warning confluence-information-macro-icon"> </span><p></p><div class="confluence-information-macro-body"><p>Showback requires the usage of either the '--start_hours_ago' or --start_time' options.</p></div></div></div></td></tr></tbody></table>