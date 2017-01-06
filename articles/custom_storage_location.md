---
title: "Custom Storage Locations"
layout: article
excerpt: Follow these steps to set up custom storage locations and access it with Synapse. 
category: howto
---

<style>
.panel.with-nav-tabs .panel-heading{
    padding: 5px 5px 0 5px;
}
.panel.with-nav-tabs .nav-tabs{
	border-bottom: none;
}
.panel.with-nav-tabs .nav-justified{
	margin-bottom: -1px;
}
</style>

# Overview
One of the main features of Synapse is to act as a repository for scientific data. Access to all data in Synapse is controlled with the use of access-control-lists (ACLs). The ACL is often the only required control on non-human subjects data. Human subjects data requires additional controls. While Synapse provides physical storage for files (using Amazon's S3), not all data 'in' Synapse is stored on Synapse controlled buckets. For example, data files can physically reside on a user owned S3 buckets, SFTP servers, or other type of file servers. Creating a custom storage location allows users ownership and control of their files, especially in cases where there is a large amount of data or cases where there are additional restrictions that need to be set on the data.


## Creating an S3 Bucket
Follow the documentation on Amazon Web Service's (AWS) site to **[Create a Bucket](http://docs.aws.amazon.com/AmazonS3/latest/gsg/CreatingABucket.html){:target="_blank"}**. Make the following adjustments to customize it to work with Synapse:  

* When you are prompted to `Create a Bucket - Select a Bucket Name and Region`, use a unique name that ends in your company domain. For example, synapse-share.yourcompany.com. For region, you must select the **`US Standard`** region.
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

For **read-write** permissions, you also need to create an object that proves to the Synapse service that you own this bucket. This can be done by creating an **owner.txt** file with your Synapse username and uploading it to your bucket or through a REST call. 

{% tabs %}

{% tab AWS %}
{% highlight bash %}
some code here
{% endhighlight %}
{% endtab %}

{% tab Command %}
{% highlight bash %}
add code here
{% endhighlight %}
{% endtab %}

{% tab Web %}
Create a new text file locally on your computer (e.g. Notepad for Windows and TextEdit for Mac) with your Synapse username. Save the file as **owner.txt**. Navigate to your bucket and select **Upload** to upload your text file.
{% endtab %}

{% endtabs %}

<br/>

* Make sure to to enable cross-origin resource sharing to allow Synapse to access your bucket.
  * Navigate to **Properties** in your bucket and click **Edit CORS configuration**
  * I
  
