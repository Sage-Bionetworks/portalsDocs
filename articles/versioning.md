---
title: Versioning
layout: article
excerpt: Learn about how versioning works on Synapse.
---

Overview
--------

After uploading a file to Synapse, you may find the need to change it (you found an error or changed the code that generates the file, for example). However, any previous version of the file should still be available - for example, if it's used in provenance relationships or part of a data release. To handle these types of situations, files re-uploaded to Synapse create a new version.

Details
-------

Only the File and Annotations of an Entity are include in the version. All other components of an Entity such as description, name, parent, ACL, and it's associated Wiki are not not part of the version, and will not vary from version to version.
