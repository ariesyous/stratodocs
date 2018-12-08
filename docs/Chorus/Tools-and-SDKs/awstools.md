# AWS Tools

## Overview

# Creating EC2 Credentials

In order to use AWS API client software outside of the system UI you need the appropriate access key and secret key.

**To obtain or generate an access key and secret key**:

1. Click  **Menu**  >  **Account Management**  >  **Access Keys**. This displays the access and secret keys for each project in your system.

2. Find the project whose keys you want and copy the access key and the secret key for that project (click the copy icon next to each key).

# Getting Started with the AWS CLI

# AWS CLI Overview

You can use the AWS CLI to interact directly with Symphony. Supported AWS services include EC2 and S3.

For example:

-   You can use the AWS CLI with the EC2 service to create a Symphony VM.
-   You can use the AWS CLI with S3 to copy a file to Symphony object storage. This can be helpful if you want to make things like images, software distributions, media files, and static HTML files available to your Symphony object storage users.

There are two ways to use AWS CLI commands with Symphony:

-   From within the Symphony GUI, you can  [use the AWS console](https://www.stratoscale.com/knowledge/use-aws-console).
-   You can also  [install and configure the AWS CLI software](https://www.stratoscale.com/knowledge/install-and-configure-aws-cli)  independent of the Symphony GUI, and use that to interact with Symphony.

# Use AWS Console

**Admin users only**

You must be an admin user to do the tasks described in this section and its sub-sections.  

From within the Symphony GUI, you can use the AWS console to run AWS CLI commands against your Symphony region.

**To use the AWS Console**:

Within the Symphony GUI, click  **Hi <user>**  (upper right corner), then click  **AWS Console**.

The AWS shell appears, and you can run AWS commands against Symphony at the  `aws>`  prompt.

Hot actions menu

You can also access the console through the  [hot actions menu](https://www.stratoscale.com/knowledge/hot-actions-menu).

Example:

Running AWS Shell

    aws> ec2 describe-images
    {
        "Images": [
            {
                "Name": "dbs_manager_mysql_5_5_002_default_v1", 
                "ImageId": "ami-1d14fdb4da924c5b87d962d487747bdc", 
                "State": "available", 
                "Architecture": "", 
                "ImageLocation": "None (dbs_manager_mysql_5_5_002_default_v1)", 
                "RootDeviceType": "ebs", 
                "OwnerId": "5870a3972fdf41dd85fdce48f7c7d373", 
                "CreationDate": "2018-02-22T19:11:56", 
                "Public": true, 
                "ImageType": "machine"
            }, 
            {
                "Name": "persistent/rootfs-centos7-workload.qcow2", 
                "ImageId": "ami-4f735f3b79a24ffd8c7286fc5b504f12", 
                "State": "available", 
                "Architecture": "", 
                "ImageLocation": "None (persistent/rootfs-centos7-workload.qcow2)", 
                "RootDeviceType": "ebs", 
                "OwnerId": "5870a3972fdf41dd85fdce48f7c7d373", 
                "CreationDate": "2018-02-22T15:07:48", 
                "Public": false, 
                "ImageType": "machine"
            }, 
            {
                "Name": "cirros-0.3.1-x86_64-disk.qcow2", 
                "ImageId": "ami-22e8f0f0290b4b5dbd9180fa02a77a92", 
                "State": "available", 
                "Architecture": "", 
                "ImageLocation": "None (cirros-0.3.1-x86_64-disk.qcow2)", 
                "RootDeviceType": "ebs", 
                "OwnerId": "5870a3972fdf41dd85fdce48f7c7d373", 
                "CreationDate": "2018-02-22T15:07:48", 
                "Public": false, 
                "ImageType": "machine"
            }, 
            {
                "Name": "persistent/trusty-server.qcow2", 
                "ImageId": "ami-b3c8012c79f44de2a63ee34b2adeeb40", 
                "State": "available", 
                "Architecture": "", 
                "ImageLocation": "None (persistent/trusty-server.qcow2)", 
                "RootDeviceType": "ebs", 
                "OwnerId": "5870a3972fdf41dd85fdce48f7c7d373", 
                "CreationDate": "2018-02-22T15:07:48", 
                "Public": false, 
                "ImageType": "machine"
            }
        ]
    }
    aws>

**Exit the console**  by pressing F10.

Copying console output

To copy console output:

Highlight the output you want to copy, then:

**Firefox**: Press Ctrl+Shift+C

**Chrome**: Press Enter

# Install and Configure AWS CLI

You can install and configure the AWS CLI software to run AWS CLI commands against Symphony.

**To use the AWS CLI with Symphony**:

1. Get your  **Symphony access key and secret key**. You will need these later when you configure AWS to talk to Symphony.

To get these keys, display the Symphony GUI. In the upper right corner, click  **Hi username**  >  **Access Keys**. Copy the values displayed for the access key and the secret key.

2.  **Dowload and install the AWS CLI**. You can get it here:

[https://aws.amazon.com/cli/](https://aws.amazon.com/cli/)

3.  **Configure the AWS CLI**. To do this, open a command window and run the  **aws configure**  command:

`$ aws configure`

This is an interactive command that prompts you to enter the following information:

	AWS Access Key ID:<Enter access key that you just got from the Symphony GUI>

	AWS Secret Access Key:<Enter secret key that you just got from the Symphony GUI>

	Default region name: <Enter "Symphony" without the quotes>

	Default output format: <Enter "table" without the quotes>

4.  **Edit the AWS config file**  to specify:

-   The access key and secret key. (You just specified these with the  **aws configure**  command, but some environments also require that these keys are present in the  `config`  file.)
-   An authentication version that will work with Symphony.

The  `config`  file is located in:

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><th class="confluenceTh">Linux</th><th class="confluenceTh">Windows</th></tr><tr><td class="confluenceTd"><code>.aws/config</code></td><td class="confluenceTd">This file is located in <code>&lt;User_home_directory&gt;/.aws/config</code>. To find your user home directory, in Windows Explorer type %UserProfile% into the search bar.</td></tr></tbody></table>

In the  `config`  file, add the following lines underneath the output and region settings:

	aws_access_key_id=<Access key that you just got from the Symphony GUI>
	aws_secret_access_key=<Secret key that you just got from the Symphony GUI>
	s3 =
	    signature_version = s3
	s3api =
	    signature_version = s3

Your final  `config`  file should look like this:

	[default]
	output = table
	region = Symphony
	aws_access_key_id=<Access key that you just got from the Symphony GUI>
	aws_secret_access_key=<Secret key that you just got from the Symphony GUI>
	s3 =
	    signature_version = s3
	s3api =
	    signature_version = s3    

5. Set each command's  **endpoint URL to the endpoint of your Symphony cluster**.

**Background**: By default, when you run an AWS CLI command, the command goes to an endpoint of:

amazonaws.com

However, to get the command to go to your Symphony cluster instead, you need to append the  `--endpoint-url <Symphony_endpoint>`  argument to each command, using the syntax:

<table class="wrapped confluenceTable"><colgroup><col><col><col></colgroup><tbody><tr><th class="confluenceTh">Service</th><th colspan="2" class="confluenceTh">Endpoint</th></tr><tr><td class="confluenceTd">EC2</td><td class="confluenceTd"><p>Symphony version 4.2.5 and later:</p><p>Earlier Symphony versions:</p></td><td class="confluenceTd"><p>https://&lt;region ip&gt;/api/v2/aws/ec2/</p><p>https://&lt;region ip&gt;/api/v2/ec2/</p></td></tr><tr><td class="confluenceTd">S3</td><td colspan="2" class="confluenceTd">https://&lt;region ip&gt;:1060/</td></tr><tr><td class="confluenceTd">RDS</td><td colspan="2" class="confluenceTd">https://&lt;region ip&gt;/api/v2/aws/rds/</td></tr><tr><td class="confluenceTd">ELB</td><td class="confluenceTd"><p>Symphony version 4.2.3 and later:</p><p>Earlier Symphony versions:</p></td><td colspan="1" class="confluenceTd"><p>https://&lt;region ip&gt;/api/v2/aws/elbv2</p><p>https://&lt;region ip&gt;/api/v2/aws/elb/</p></td></tr></tbody></table>

**How to get the region IP of the Symphony cluster**

From within the GUI click  **Menu** > **Region Monitoring** > **Overview**. The Overview panel displays the IP of the cluster.

For example, assume that:

-   The IP of your Symphony cluster is 10.10.100.10
-   You have an object store bucket on that cluster called MyBucket.
-   You have a file called `test.txt`  that you want to copy to that bucket.

You can run the following S3 command to copy the file to the Symphony bucket:

	$ aws s3 cp test.txt s3://MyBucket/ --endpoint-url http://10.10.100.10:1060

	upload: .test.txt to s3://MyBucket/test.txt

SSL troubleshooting tip

If you encounter this error:

`[Errno 1] _ssl.c:504: error:14090086:SSL routines:SSL3_GET_SERVER_CERTIFICATE:certificate verify failed`

You may also need to add the following argument:

`--no-verify-ssl`