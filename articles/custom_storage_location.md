---
title: "Custom Storage Locations"
layout: article
excerpt: Follow these steps to set up custom storage locations and access it with Synapse. 
category: howto
---

<style>
#image {
    width: 100%;
}
</style>

# Overview
One of the main features of Synapse is to act as a repository for scientific data. Access to all data in Synapse is controlled with the use of access-control-lists (ACLs). The ACL is often the only required control on non-human subjects data. Human subjects data requires additional controls. While Synapse provides physical storage for files (using Amazon's S3), not all data 'in' Synapse is stored on Synapse controlled buckets. For example, data files can physically reside on a user owned S3 buckets, SFTP servers, or other type of file servers. Creating a custom storage location allows users ownership and control of their files, especially in cases where there is a large amount of data or cases where there are additional restrictions that need to be set on the data.

## Using SFTP

## Setting Up an External Bucket
Follow the documentation on Amazon Web Service's (AWS) site to **[Create a Bucket](http://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html){:target="_blank"}**. 

<a href="http://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html" class="btn btn-primary">View AWS Bucket Instructions</a>{:target="_blank"}

Make the following adjustments to customize it to work with Synapse:  

* When the AWS instructions prompt you to `Create a Bucket - Select a Bucket Name and Region`, use a unique name that ends in your company domain. For example, synapse-share.yourcompany.com. For region, you must select the **`US Standard`** region.
* Select the newly created bucket and click the **Properties** button. Expand the **Permissions** section and:  
    * Make sure that all the boxes (List, Upload/Delete, View Permissions, and Edit Permissions) have been checked. It should do this by default. 
    * Select the **Add bucket policy** button and copy one of the below policies (read-only or read-write permissions). Change the name of `Resource` from “synapse-share.yourcompany.com” to the name of your new bucket (twice) and ensure that the `Principal` is `"AWS":"325565585839"`. This is Synapse's account number. 

For **read-only** permissions (you only allow Synapse to read files that you upload to this bucket):

````
# READ-ONLY PERMISSIONS

{
    "Statement": [
        {
            "Action": "s3:ListBucket*",
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::synapse-share.yourcompany.com",
            "Principal": { "AWS": "325565585839" }
        },
        {
            "Action": [ "s3:GetObject*", "s3:*MultipartUpload*" ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::synapse-share.yourcompany.com/*",
            "Principal": { "AWS": "325565585839" }
        }
    ]
}
````

For **read-write** permissions (you allow Synapse to upload and retrieve files):

````
# READ-WRITE PERMISSIONS

{
    "Statement": [
        {
            "Action": "s3:ListBucket*",
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::synapse-share.yourcompany.com",
            "Principal": { "AWS": "325565585839" }
        },
        {
            "Action": [ "s3:*Object*", "s3:*MultipartUpload*" ],
            "Effect": "Allow",
            "Resource": "arn:aws:s3:::synapse-share.yourcompany.com/*",
            "Principal": { "AWS": "325565585839" }
        }
    ]
}
````

For **read-write** permissions, you also need to create an object that proves to the Synapse service that you own this bucket. This can be done by creating an **owner.txt** file with your Synapse username and uploading it to your bucket. You can upload the file with our Synapse web client or if you have  the [AWS command line client](https://aws.amazon.com/cli/){:target="_blank"}, you can upload using the command line. 

{% tabs %}

{% tab AWScli %}
{% highlight bash %}
# copy your owner.txt file to your s3 bucket
aws s3 cp owner.txt s3://nameofmybucket/nameofmyfolder
{% endhighlight %}
{% endtab %}

{% tab Web %}
Create a new text file locally on your computer (e.g. Notepad for Windows and TextEdit for Mac) with your Synapse username. Save the file as **owner.txt**. Navigate to your bucket and select **Upload** to upload your text file.
{% endtab %}

{% endtabs %}

<br/>


### Set S3 Bucket as Upload Location

By default, your `Project/Folder` uses Synapse storage. You can use the external bucket configured above via the web client or our REST API.

{% tabs %}

{% tab Python %}
{% highlight python %}
# Create a dictionary of your bucket name along with the concrete type
foo = '{"bucket":"nameofbucket", "concreteType"="org.sagebionetworks.repo.model.project.ExternalS3StorageLocationSetting"}'
# Set upload location
bar = syn.restPOST("./storageLocation", body=foo)
{% endhighlight %}
{% endtab %}

{% tab R %}
{% highlight r %}
# Create a dictionary of your bucket name along with the concrete type
foo <- list(bucket = "nameofbucket", concreteType = "org.sagebionetworks.repo.model.project.ExternalS3StorageLocationSetting")
# Set upload location
bar <- synRestPOST("/storageLocation", body=foo)
{% endhighlight %}
{% endtab %}

{% tab Web %}
Navigate to your **Project/Folder -> Tools -> Change Storage Location**. In the resulting pop-up, select the `Amazon S3 Bucket` option and fill in the relevant information, where Bucket is the name of your external bucket, Base Key is the name of the folder in your bucket to upload to, and Banner is a short description such as who owns the storage location:
  
<img id="image" src="/assets/images/external_s3.png">
{% endtab %}

{% endtabs %}

<br/>

Please see the [REST docs](http://docs.synapse.org/rest/org/sagebionetworks/repo/model/project/ExternalS3StorageLocationSetting.html){:target="_blank"} for more information on external storage location settings.

## Using a File-Proxy

For files stored outside of Amazon, an additional proxy is needed to validate the pre-signed URL and then proxy the requested file contents. The primary purpose of this project is to provide such validation and file proxying.  View more information **[here](https://github.com/Sage-Bionetworks/file-proxy/wiki){:target="_blank"}** about setting up a file-proxy.

### Connecting Synapse to the Restricted Filesystem

You must have a key ("your_sftp_key") to allow Synapse to interact with the filesystem:

```python
import synapseclient
import json
syn = synapseclient.login()
PROJECT = 'syn12345'
destination = {"uploadType":"SFTP", 
               "secretKey":"your_sftp_key", 
               "proxyUrl":"https://your-proxy.prod.sagebase.org", 
               "concreteType":"org.sagebionetworks.repo.model.project.ProxyStorageLocationSettings"}
destination = syn.restPOST('/storageLocation', body=json.dumps(destination))
project_destination ={"concreteType": "org.sagebionetworks.repo.model.project.UploadDestinationListSetting", 
                      "settingsType": "upload"}
project_destination['locations'] = destination['storageLocationId']
project_destination['projectId'] = PROJECT
project_destination = syn.restPOST('/projectSettings', body = json.dumps(project_destination))
```

#### Create a Filehandle

A filehandle is merely a Synapse representation of the file, therefore you will have to specify all the metadata below for Synapse to recognize it.

```python
import mimetypes
path='/path/to/your/file.txt'
fileType = mimetypes.guess_type(path,strict=False)[0]
fileHandle = {'concreteType': 'org.sagebionetworks.repo.model.file.ProxyFileHandle',
              'fileName'    : os.path.basename(path),
              'contentSize' : "2252439673",
              'filePath' : path,
              'contentType' : fileType,
              'contentMd5' :  '67a3688466ad3f606e2cc7b42df4d4bb',
              'storageLocationId': destination['storageLocationId']}
fileHandle = syn.restPOST('/externalFileHandle/proxy', json.dumps(fileHandle), endpoint=syn.fileHandleEndpoint)
f = synapseclient.File(parentId=PROJECT, dataFileHandleId = fileHandle['id'])
f = syn.store(f)
```

