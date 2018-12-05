
# Object Storage

## What is object storage? 

Symphony object storage is a simple storage mechanism where you place a "file" (object) in a "self storage unit" bucket and have an access key. Anyone who has access to the storage unit can use the key to retrieve a copy of the object. Object storage is compatible with the AWS S3 service.

The user does not care where the object is actually stored, what the format of the object is, or the size of the bucket - none of these things is exposed to the user.

Instead, the user employs known the known web protocols HTTP / HTTPS to upload and download objects. This is an operating system agnostic protocol.

The user can use a simple browser or many other common S3 tools.

# Set up and use object storage

**Admin users only**

To set up object storage for the first time you must be an Admin user in the Stratoscale Symphony region.

Functionality is exposed:

-   In the GUI under  **Menu**  >  **Storage**  >  **Object Storage**.
-   In the CLI:
    -   Admin functionality for using the  `symp`  client to work with object stores is exposed in the [`object-stores`commands](https://www.stratoscale.com/knowledge/object-stores).
    -   End user functionality is exposed by using the  [AWS CLI for S3](http://docs.aws.amazon.com/cli/latest/userguide/using-s3-commands.html).

**Required administrator task - initialize service and create object store**

Before users can use object storage features, an administrator must initialize the object storage service.

To do this:

1. Click  **Menu**  >  **Storage**  >  **Object Storage**  >  **Initialize**.

The system initializes the object storage system.

2. The Create Object Store window appears.

Specify  **Storage Pool**  and  **Size**  (in GB).

This is the object store for the  **entire**  Symphony region, so be sure to allocate resources accordingly.

If you need to change the object store later on...

If you need to change the size of the object store later on, you can use the Symphony CLI to delete the existing object store and create a new one. However, be aware that you will lose all the data in the original object store.

To delete an existing object store and create a new one first log in as an Admin user via Symphony CLI:

 To find the ID of the existing object store
    
    Symphony @ cloud_admin/default > object-stores list
    +--------+--------------------------------------+
    | status | mancala_volume_id                    |
    +--------+--------------------------------------+
    | Ready  | b1638b75-67fb-4f01-a196-3e0408079710 |
    +--------+--------------------------------------+
    
To delete the existing object store
    
    Symphony @ cloud_admin/default > object-stores delete {object_store_id / b1638b75-67fb-4f01-a196-3e0408079710}
    
 To create a new object store
    
    Symphony @ cloud_admin/default > object-stores create --storage-pool <STORAGE_POOL_NAME> --size-mb <SIZE_IN_MB>



# Objects and Buckets

Creating and deleting  **buckets**:

-   Users can create containers (buckets) where they can place objects.
-   Users can delete empty buckets.

When working with  **objects**, users can:

-   Upload an object.
-   Download an object.
-   Delete an object.
-   List the objects in a bucket.

Users can not modify an object.

# How Object Storage is Consumed

How does the end user consume object storage?

-   CLI
-   API - use the AWS S3 API.
-   GUI - An abstraction of the buckets/folders/files tree structure, for ease of use. Folders are not really part of an object store, but similar to AWS Symphony uses ‘/’ in the key names to group objects into folders in the GUI.

# Use Cases

What is object storage used for?

-   To share data between VMs or between 3rd party software or even users.
    
    All data access is via the GUI or the API, so location is not a barrier.
    
-   For simple persistent storage.
    
    Abstracts away all complexity and considerations, like file size, free storage, which disk to use, backups, etc.
    

Many use cases:

-   Data at rest - data that is not often accessed like archives, backups, big data ETL.
-   Event driven processing - one component writes data, another one triggered and processed it.
-   Key-Value store for applications.
-   Sharing documents between applications and users.

![](https://www.stratoscale.com/wp-content/uploads/object_storage.png)

# Symphony-supported AWS – S3 APIs

Below is a list of the AWS - S3 APIs that Symphony supports. All request  **Parameters**  and  **Elements**  for each API are supported.

All request **Headers**  for each API are supported, unless indicated otherwise in the column next to the API.

Click on the API name to access the complete AWS documentation for that action.

<table class="wrapped confluenceTable"><colgroup><col><col></colgroup><tbody><tr><td class="highlight-grey confluenceTd" data-highlight-colour="grey"><strong>Service Operation</strong></td><td class="highlight-grey confluenceTd" data-highlight-colour="grey"><strong>Unsupported Headers</strong></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTServiceGET.html" rel="nofollow">GET Service</a></td><td class="confluenceTd"></td></tr><tr><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>Bucket Operations</strong></td><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>Unsupported Headers</strong></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketDELETE.html" rel="nofollow">DELETE Bucket</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketDELETEcors.html" rel="nofollow">DELETE Bucket cors</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><div><div><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketDELETEreplication.html" rel="nofollow">DELETE Bucket replication</a></div></div></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketDELETEwebsite.html" rel="nofollow">DELETE Bucket website</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><div><div><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/v2-RESTBucketGET.html" rel="nofollow">GET Bucket (List Objects) Version 2</a></div></div></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETacl.html" rel="nofollow">GET Bucket acl</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETcors.html" rel="nofollow">GET Bucket cors</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETlocation.html" rel="nofollow">GET Bucket location</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><div><div><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETVersion.html" rel="nofollow">GET Bucket Object versions</a></div></div></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETreplication.html" rel="nofollow">GET Bucket replication</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETversioningStatus.html" rel="nofollow">GET Bucket versioning</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketGETwebsite.html" rel="nofollow">GET Bucket website</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketHEAD.html" rel="nofollow">HEAD Bucket</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadListMPUpload.html" rel="nofollow">List Multipart Uploads</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUT.html" rel="nofollow">PUT Bucket</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTacl.html" rel="nofollow">PUT Bucket acl</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTcors.html" rel="nofollow">PUT Bucket cors</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTreplication.html" rel="nofollow">PUT Bucket replication</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTVersioningStatus.html" rel="nofollow">PUT Bucket versioning</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTBucketPUTwebsite.html" rel="nofollow">PUT Bucket website</a></td><td class="confluenceTd"></td></tr><tr><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>Object Operations</strong></td><td class="highlight-grey confluenceTd" colspan="1" data-highlight-colour="grey"><strong>Unsupported Headers</strong></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/multiobjectdeleteapi.html" rel="nofollow">Delete Multiple Objects</a></td><td class="confluenceTd"><p></p></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectDELETE.html" rel="nofollow">DELETE Object</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectDELETEtagging.html" rel="nofollow">DELETE Object tagging</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectGET.html" rel="nofollow">GET Object</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectGETacl.html" rel="nofollow">GET Object ACL</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectGETtagging.html" rel="nofollow">GET Object tagging</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectHEAD.html" rel="nofollow">HEAD Object</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectPUT.html" rel="nofollow">PUT Object</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption</li><li>x-amz-server-side-encryption-aws-kms-key-id</li><li>x-amz-server-side-encryption-context</li><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectCOPY.html" rel="nofollow">PUT Object - Copy</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption</li><li>x-amz-server-side-encryption-aws-kms-key-id</li><li>x-amz-server-side-encryption-context</li><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectPUTacl.html" rel="nofollow">PUT Object acl</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/RESTObjectPUTtagging.html" rel="nofollow">PUT Object tagging</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadAbort.html" rel="nofollow">Abort Multipart Upload</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><div><div><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadComplete.html" rel="nofollow">Complete Multipart Upload</a></div></div></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadInitiate.html" rel="nofollow">Initiate Multipart Upload</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption</li><li>x-amz-server-side-encryption-aws-kms-key-id</li><li>x-amz-server-side-encryption-context</li><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadListParts.html" rel="nofollow">List Parts</a></td><td class="confluenceTd"></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadUploadPart.html" rel="nofollow">Upload Part</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr><tr><td class="confluenceTd"><a class="external-link" href="http://docs.aws.amazon.com/AmazonS3/latest/API/mpUploadUploadPartCopy.html" rel="nofollow">Upload Part - Copy</a></td><td class="confluenceTd"><ul><li>x-amz-server-side-encryption</li><li>x-amz-server-side-encryption-aws-kms-key-id</li><li>x-amz-server-side-encryption-context</li><li>x-amz-server-side-encryption-customer-algorithm</li><li>x-amz-server-side-encryption-customer-key</li><li>x-amz-server-side-encryption-customer-key-md5</li></ul></td></tr></tbody></table>




