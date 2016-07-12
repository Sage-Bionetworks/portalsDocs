---
title: Versioning
layout: article
excerpt: Learn about how versioning works on Synapse.
---

Overview
========

After uploading a file to Synapse, you may find the need to change it. For example, you modified the code that creates the file, changing it's contents. Or, you found an error and needed to make a manual change. Uploading new versions of a file to replace an existing one in Synapse is the answer.

It is important to note that, by default, any previous versions of the file should still be available - it may be used in provenance relationships or as part of a data release. To handle these types of situations, files re-uploaded to Synapse create a new version.

Details
=======

Versioning is an important component to reusable, reproducible research. There are a number of ways that versioning can be accomplished, including the commonly used filename modification scheme (e.g., 'file.txt', 'file-1.txt', 'file-1a.txt', 'file-final.txt', and then 'file-reallyfinal.txt'). However, this is less than satisfactory for a number of reasons. First, the rules for naming are arbitrary, and may change over time. Second, it is not possible to easily determine (without external documentation) that this set of file changes are related to the same file. Third, it becomes difficult to manage future use of specific versions of the file. Using `File` versioning provided by Synapse solves these issues.

When a Synapse `File` is initially stored, it automatically gets a version of `1`. It can be referred to explicitly by it's Synapse ID: `syn12345678.1`. If the contents of a file are changed and you indicate that you want to replace an existing Synapse `File` with a new one (through the web interface from the Tools menu by selecting 'Upload a New Version of the File', or through the programmatic clients), the Synapse ID will remain but the version will increase, e.g., `syn12345678.2`. Hence, this is a standard, transparent way to determine how a file has changed and the relationship over time between the versions. It also provides a single entry point (the Synapse ID, `syn12345678`) to find the file and determine if there are multiple versions. Further, it allows for downstream use of specific versions of the `File`, and other users can always come back to see if new verions exist and have been subsequently processed as well.

Providing the Synapse ID without any versioning information to any of the clients (e.g., `syn12345678`) will always point to the most recent version of the file. In this way, updates to files can be automatically fetched by users by simply omitting the version.

If a DOI has been created for a Synapse file, it is automatically versioned as well, so specific versions can be cited in other places.

The easiest way to create a new version of an existing Synapse `File` is to use the same file name and store it in the same location (e.g., the same `parentId`). Synapse will automatically determine that a new version of a file is being stored, only if the contents of the file have changed. If the contents have not changed (e.g., the `md5sum` of the file is identical to the most recent version), a new file will not be uploaded and the version will not increase.

Only the file and annotations information are included in the version. Other metadata about a Synapse `File` (such as the description, name, parent, ACL, *and it's associated Wiki*) are not not part of the version, and will not change between versions.
