
# Symphony Client Overview

The Symphony client is called  `symp`. You use the  `symp`  client to run  [Symphony CLI commands](https://www.stratoscale.com/knowledge/symphony-cli-reference).

There are two ways to use the  `symp`  CLI commands with Symphony:

-   From within the Symphony GUI, you can use the  [SYMP console](https://www.stratoscale.com/knowledge/use-symp-console).
-   You can also  [install the symp client on an external Lixux machine](https://www.stratoscale.com/knowledge/install-symphony-client-on-external-machine).
# Use SYMP Console

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

From within the Symphony GUI, you can use the SYMP console to run  `symp`  commands against your Symphony region.

**To use the SYMP Console**:

Within the Symphony GUI, click  **Hi <user>**  (upper right corner), then click  **SYMP Console**.

The Symphony shell appears, and you can run  `symp`  commands against at the  `Symphony>`  prompt.

Hot actions menu

You can also access the console through the  [hot actions menu](https://www.stratoscale.com/knowledge/hot-actions-menu).

Example:

    Symphony > image list -f json
    [
      {
        "status": "ready", 
        "info": "", 
        "description": "{'version': 'v1', 'name': 'dbs_manager_mysql_5_5_002_default'}", 
        "tags": [
          "system:dbs-manager", 
          "system:managed"
        ], 
        "sourceId": "", 
        "projectID": "5870a3972fdf41dd85fdce48f7c7d373", 
        "isPublic": true, 
        "userID": "admin", 
        "properties": {}, 
        "storagePool": "caffcbca-8160-4700-8255-6a883249dab6", 
        "deletedAt": "", 
        "size": 3.0, 
        "id": "1d14fdb4-da92-4c5b-87d9-62d487747bdc", 
        "createdAt": "2018-02-22T19:11:56", 
        "name": "dbs_manager_mysql_5_5_002_default_v1"
      }, 
      {
        "status": "ready", 
        "info": "", 
        "description": null, 
        "tags": [], 
        "sourceId": "", 
        "projectID": "5870a3972fdf41dd85fdce48f7c7d373", 
        "isPublic": false, 
        "userID": "admin", 
        "properties": {}, 
        "storagePool": "caffcbca-8160-4700-8255-6a883249dab6", 
        "deletedAt": "", 
        "size": 16.0, 
        "id": "4f735f3b-79a2-4ffd-8c72-86fc5b504f12", 
        "createdAt": "2018-02-22T15:07:48", 
        "name": "persistent/rootfs-centos7-workload.qcow2"
      }, 
      {
        "status": "ready", 
        "info": "", 
        "description": null, 
        "tags": [], 
        "sourceId": "", 
        "projectID": "5870a3972fdf41dd85fdce48f7c7d373", 
        "isPublic": false, 
        "userID": "admin", 
        "properties": {}, 
        "storagePool": "caffcbca-8160-4700-8255-6a883249dab6", 
        "deletedAt": "", 
        "size": 1.0, 
        "id": "22e8f0f0-290b-4b5d-bd91-80fa02a77a92", 
        "createdAt": "2018-02-22T15:07:48", 
        "name": "cirros-0.3.1-x86_64-disk.qcow2"
      }, 
      {
        "status": "ready", 
        "info": "", 
        "description": null, 
        "tags": [], 
        "sourceId": "", 
        "projectID": "5870a3972fdf41dd85fdce48f7c7d373", 
        "isPublic": false, 
        "userID": "admin", 
        "properties": {}, 
        "storagePool": "caffcbca-8160-4700-8255-6a883249dab6", 
        "deletedAt": "", 
        "size": 3.0, 
        "id": "b3c8012c-79f4-4de2-a63e-e34b2adeeb40", 
        "createdAt": "2018-02-22T15:07:48", 
        "name": "persistent/trusty-server.qcow2"
      }
    ]

**Exit the console**  by typing exit.

Copying console output

To copy console output:

Highlight the output you want to copy, then:

**Firefox**: Press Ctrl+Shift+C

**Chrome**: Press Enter

# Install Symphony Client on External Machine

The Symphony client is called  `symp`. You use the  `symp`  client to run  [Symphony CLI commands](https://www.stratoscale.com/knowledge/symphony-cli-reference). You should install the  `symp`  client on a Linux machine that is external to your Symphony cluster.

You can install the  `symp`  client in the following environments:

-   Ubuntu
-   Debian
-   Fedora
-   RHEL
-   CentOS

**To install the symp client on an external Linux machine**:

1.  **Install dependencies**:
<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="confluenceTd"><strong>Ubuntu/Debian</strong></td><td class="confluenceTd"><div class="content-wrapper"><div class="code panel pdl conf-macro output-block" data-hasbody="true" data-macro-name="code" style="border-width: 1px;"><div class="codeContent panelContent pdl"><pre class="syntaxhighlighter-pre" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence">$ sudo apt-get update
$ sudo apt-get install python-pip
$ sudo apt-get install unzip</pre></div></div></div></td></tr><tr><td colspan="1" class="confluenceTd"><strong>Fedora/RHEL/CentOS</strong></td><td colspan="1" class="confluenceTd"><div class="content-wrapper"><div class="code panel pdl conf-macro output-block" data-hasbody="true" data-macro-name="code" style="border-width: 1px;"><div class="codeContent panelContent pdl"><pre class="syntaxhighlighter-pre" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence">$ sudo yum clean all
$ sudo yum install python-pip
$ sudo yum install unzip</pre></div></div></div></td></tr></tbody></table>

2.  **Get the symp client installer**:

	    $ sudo URL=https://<ip_of_symphony_region> bash -c "$(curl -sSLk https://<ip_of_symphony_region>/install-client.sh)"
	    
	    
	    Using target cluster url https://<ip_of_symphony_region>
	    Downloading client code...
	    replace /opt/symphony-client/symphony_client/__main__.py? [y]es, [n]o, [A]ll, [N]one, [r]ename: Creating symp binary...
	    Defining environment variables...
	    Installing required pip packages...
	    Collecting cliff
	      Using cached cliff-2.11.0-py2-none-any.whl
	    Collecting debtcollector
	      Using cached debtcollector-1.19.0-py2.py3-none-any.whl
	    Requirement already satisfied: stevedore>=1.20.0 in /usr/lib/python2.7/site-packages (from cliff)
	    Requirement already satisfied: pbr!=2.1.0,>=2.0.0 in /usr/lib/python2.7/site-packages (from cliff)
	    Collecting cmd2>=0.6.7 (from cliff)
	    Requirement already satisfied: PrettyTable<0.8,>=0.7.1 in /usr/lib/python2.7/site-packages (from cliff)
	    Collecting unicodecsv>=0.8.0; python_version < "3.0" (from cliff)
	    Requirement already satisfied: six>=1.10.0 in /usr/lib/python2.7/site-packages (from cliff)
	    Requirement already satisfied: pyparsing>=2.1.0 in /usr/lib/python2.7/site-packages (from cliff)
	    Requirement already satisfied: PyYAML>=3.10 in /usr/lib64/python2.7/site-packages (from cliff)
	    Collecting funcsigs>=1.0.0; python_version == "2.7" or python_version == "2.6" (from debtcollector)
	      Using cached funcsigs-1.0.2-py2.py3-none-any.whl
	    Collecting wrapt>=1.7.0 (from debtcollector)
	    Requirement already satisfied: contextlib2 in /usr/lib/python2.7/site-packages (from cmd2>=0.6.7->cliff)
	    Requirement already satisfied: pyperclip in /usr/lib/python2.7/site-packages (from cmd2>=0.6.7->cliff)
	    Collecting subprocess32 (from cmd2>=0.6.7->cliff)
	      Using cached subprocess32-3.2.7.tar.gz
	    Building wheels for collected packages: subprocess32
	      Running setup.py bdist_wheel for subprocess32 ... done
	      Stored in directory: /root/.cache/pip/wheels/7d/4c/a4/ce9ceb463dae01f4b95e670abd9afc8d65a45f38012f8030cc
	    Successfully built subprocess32
	    Installing collected packages: subprocess32, cmd2, unicodecsv, cliff, funcsigs, wrapt, debtcollector
	    Successfully installed cliff-2.11.0 cmd2-0.8.0 debtcollector-1.19.0 funcsigs-1.0.2 subprocess32-3.2.7 unicodecsv-0.14.1 wrapt-1.10.11
	    
	    Installation finished successfully!

Run symp to connect to Symphony cluster

3.  **Run a  `symp`  command to verify**:

		$ symp -k -u admin -d cloud_admin -p admin --url https://<ip_of_symphony_region> image list -c name
	    
	    Starting new HTTPS connection (1): demo10.stratoscale.com
	    Connecting in insecure mode!
	    Failed loading virt-network commands
	    
	    +---------------------------------------------------------------------------------------------+
	    | name                                                                                        |
	    +---------------------------------------------------------------------------------------------+
	    | image_bitnami-jenkins-1.658-4-linux-ubuntu-14.04-x86_64765fbc84-7fa9-4bf3-9099-1d4a943982d4 |
	    | dbs_manager_mysql_5_6_001_default_v1                                                        |
	    | linux                                                                                       |
	    | dbs_manager_mysql_5_7_001_default_v1                                                        |
	    | centos1711                                                                                  |
	    | image_bitnami-mysql-5.6.33-3-linux-ubuntu-14.04-x86_64f65a83e6-1fac-442e-9c0a-f0364c9e7905  |
	    | webserver-centos1                                                                           |
	    | centos7-1708                                                                                |
	    | dbs_manager_mariadb_10_1_001_default_1.0                                                    |
	    | mapreduce_manager_mapreduce_1_2_001_default_1.0                                             |
	    | image_bitnami-jenkins-1.658-4-linux-ubuntu-14.04-x86_64faba5616-46ce-4e52-81e8-26b3f5572327 |
	    | windows2012                                                                                 |
	    | image_bitnami-jenkins-1.658-4-linux-ubuntu-14.04-x86_643b70fd8c-082f-4ccc-8e82-f0a1bf534c3f |
	    | dbc_manager_cassandra_3_11_001a_default_1.0                                                 |
	    | dbs_manager_postgresql_9_6_000_default_v1                                                   |
	    | kubernetes-base_v1.8.1                                                                      |
	    | dbs_manager_mysql_5_5_001_default_v1                                                        |
	    | cirros-0.4.0-x86_64-disk.img                                                                |
	    | webserver-centos2                                                                           |
	    | dbc_manager_cassandra_3_0_004_default_1.0                                                   |
	    | image_bitnami-elk-4.6.1-0-linux-ubuntu-14.04-x86_649d0a3261-9e7d-4063-a0f0-13a3d77a2b47     |
	    | nfs_manager_nfs_1_0_002_default_1.0                                                         |
	    | lbaas-engine_v2                                                                             |
	    +---------------------------------------------------------------------------------------------+

