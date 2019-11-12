---
title: "Sharing Settings"
layout: article
excerpt: Sharing settings determine who can access content in Synapse.
category: governance
order: 2
---

## Access Control

Synapse has two ways to control who can access your content. `Sharing Settings`, or permissions, determine _who_ can access content and at what level. `Conditions for Use` define _how_ users with access may use the data. All content in Synapse has Sharing Settings but not all content has Conditions for Use. See the [Conditions for Use](/articles/access_control.html) article for information about those settings. This article covers sharing settings only.

<a name="sharing-setting"></a>

## Sharing Settings

You can use the `Sharing Settings` to grant different levels of access to individuals or `Teams`. Often, users leverage these features to invite people to view or collaborate on a Synapse `Project`. Sharing Settings can apply to an entire project or for individual files or folders within a project.

There are two primary groups: **Public** and **Private**. The `Private` sharing setting limits access to only specified users and teams. By default, new projects are `Private`. The `Public` sharing setting applies to users on the web and any registered, logged-in Synapse user.

When sharing with specific users and teams, Synapse supports the following permissions: view, download, edit, edit/delete, and administrator.

### View permissions

View permissions give a Synapse user the ability to see that something in Synapse exists (like a Project, File, or Folder). They can discover it using Synapse search, and it will be visible to them if included in a [View](articles/views.html). If there are [annotations](https://docs.synapse.org/articles/annotation_and_query.html) associated with it, they can see these as well. They cannot see the contents of a File, including if a preview of the file is available in the web. View permissions are the only permissions that can be granted to the public (anonymous users).

### Download permissions

Download permissions give a Synapse user the ability to see the contents of a File entity and download the file to their own computer. Having download permissions includes also having view permissions.

### Edit permissions

Edit permissions allows a Synapse user to make changes to something in Synapse. Edit permissions are cumulative with view and download permissions. A user with edit permissions can:

- change the name of an entity.
- [change the annotations](/articles/annotation_and_query.html#modifying-annotations) associated with an entity, including removing existing annotations.
- [create a new version](/articles/files_and_versioning.html#uploading-a-new-version) of a file
- make changes to a [Wiki](/articles/wikis.html).
- [change the storage location settings](/articles/custom_storage_location.html) of a Project or Folder.

A user with edit permissions cannot delete the entity shared with them.

### Edit and delete permissions

Edit and delete permissions allows a user to delete an entity shared with them, in addition to the edit permissions previously described. Edit and delete permissions are cumulative with view and download permissions.

### Administrator permissions

Administrator permissions allows a Synapse user to change the sharing settings and metadata related to an entity. They can change the friendly URL of a project. They can add, remove, or modify the sharing settings of an entity, including removing themself. Administrator permissions are cumulative with edit and delete permissions.

{% include important.html content="Synapse users are responsible for determining the appropriate Sharing Setting for any content they upload into Synapse." %}

<a name="how-to-share-content"></a>

## How to Share Projects

To adjust the sharing settings on a project, click the `Project Settings` button. This will open a window listing the Synapse users who have access to the `Project` and their roles. When you create a new `Project` you are the only Synapse user listed in this window, because projects are private by default, and your access level will be `Administrator`.

Use the `Add People` feature to add collaborators individually or to add a [team of collaborators](teams.md).

<a name="share-files-folders-and-tables"></a>

## Sharing Files, Folders, and Tables

You can adjust the sharing settings for `Folders`, `Files`, and `Tables` separately from their parent project. For example, you may wish to keep a particular folder private while you make the project public. Or you may want to share drafts of individual files to collaborators first prior to sharing them publicly.

By default, all of the content residing within a project inherits the project sharing settings. You can override this inheritance by defining a `Local Sharing Setting` for that specific content. To do so, visit the content in question (Folder, File, or Table). Click on the `Tools` menu, and then click on the `Sharing Setting` option for that content. The menu option will show the type of content, e.g. `Folder Sharing Settings` or `File Sharing Settings`, etc.).

When you click on the sharing settings for that content, you'll see the current (inherited) sharing settings. You will also see the option to `Create Local Sharing Settings`. Once you create the local sharing settings, you'll be able to change them to be different than the parent project.

## Sharing Wikis and Discussion Forums

Note you **cannot** set local sharing settings for `Wikis` and `Discussion Forums`. These areas can only inherit the sharing settings from their parent project.
