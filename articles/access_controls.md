---
title: "Access and Content Restrictions"
layout: article
excerpt: Learn how to share and restrict content on Synapse using the sharing settings and conditions for use. 
---

## Access and Content Restrictions
Synapse content is subject to two control settings: the `Sharing setting` and `Conditions for Use.` The `Sharing setting` determines _with whom_ content is shared. `Conditions for Use` govern _how_ content can be used. 

## Sharing setting
The `Sharing setting` enables you to invite others to view or collaborate on a project you have created. Projects can be **Public** visible to all or **Private** and visible to selected few. Public projects and contents are shared **broadly** with all registered Synapse users while Private projects and content are shared **sparsely**, with a limited set of designated users (e.g., a team) or not shared at all. **By default, your newly created project is private;** you are the only person that can access it or any content included in it. You can use the `Sharing setting` to enable others to view the content of your projects.
{% include important.html content="Users are responsible for determining the appropriate Sharing Setting for any content they upload into Synapse." %}

#### Create a team
If you want to share a project with a specific group of people, you can create a team. Any Synapse user can create a team and invite other Synapse users to join their team. Only after the invited user accepts this invitation is he/she added to the team. Similarly, any Synapse user can request to be added to a team.

### How to share content
To give others access to your project and its content, click on the Share icon in the upper right hand corner of the screen. One of two icons will be displayed: either a globe, meaning the project is shared broadly (public), or a lock, meaning that the project is private and only visible to investigators you have authorized. Clicking on the lock will open a window listing the users who have access to the private project and their roles/privileges.


![sharing button examples]({{site.url}}/assets/images/sharing_buttons_examples.png)

### Sharing content within a project 
By default, all content residing within a project **inherits** the project `Sharing settings` that you specify for the project. For example if you upload a new file in a public project, the file will also be Public. You may change this for any folder, file or table by creating a local `Sharing setting`. Note that `Wikis` and `Discussion Forum` cannot be assigned local sharing setting.
If you change the `Sharing setting` on a folder all content within that folder will inherit that change. Just as your are able to control who can access your project, you can also restrict or open portions of your project using the Sharing setting for a folder or subfolder. To set up local Sharing settings select the Share icon from the chosen Project, Folder, File or Table.
Inheritance is illustrated in the example below. In the diagram, the projects A and B carry the “share broadly” (public) `Sharing setting` designated by the globe icon. No local sharing settings are shown for folders 1 and 2 and Table 3 in Project A. Since these folders and table do not have a Sharing setting specified, they inherit the `sharing setting` of the project: “share broadly.” By contrast, in Project B the folder 4 and Table 6 have a restricted `Sharing setting`, designated with the lock icon. File 5 has no local sharing setting and therefore it inherits the `sharing setting` of the project: “share broadly.” It is important to note that if you were to move File 5into the restricted Folder 4 then File 5’s Sharing setting will be reset to the restricted Sharing settingof Folder 4: “share sparsely”.

<img src= "/assets/images/synapse_sharingsetting.jpg">

## Conditions for Use<a name="conditions_of_use"></a>
`Conditions for Use` indicate how content can be used. `Conditions for Use` are added to human data that require additional protection based on its type, source and/or collection method. For example, human 'omic' data may have `Conditions for Use` imposed by informed consent requirements, legal contracts, or other privacy requirements. It is also appropriate to add `Condition for Use` to data collected from "vulnerable" population or to content that could potentially harm individuals or groups if misused.
{% include important.html content="Controlled data may not be redistributed." %}
Controlled data can only be used by authorized investigators and are not transferable (unless explicitly specified otherwise). In other words, you cannot share Controlled data with collaborators unless they have been approved to use the data. Each Synapse users wishing to access Controlled Use data must individually agree to the `Conditions for Use` for that data.
{% include important.html content="Investigators are responsible for determining the appropriate Conditions for Use for any data they upload into Synapse." %}
It is important to note that `Conditions for Use` cannot be set for Synapse wiki or discussion forum. These are not designed to house data and therefore do not have local `Conditions for Use` as a feature. Synapse wikis and discussion forum inherit the condition for Use of their parent project.

### Data that does not require Conditions for Use

Open Data in Synapse are data without `Conditions for Use.` They can be used by any registered Synapse users authorized to view the project/folder/file/table (based on sharing setting) for research purpose. Typically Open Data are:

* Data from model organism, species or strain
* Non-biological data such as presentations, results or images

Human data that are:
* Publicly available elsewhere
* Anonymous data
* De-identified non-sensitive data with no known sharing or use restrictions
* Self-contributed data unambiguously consented for open data sharing and use

### Data that does require Conditions for Use (“Controlled Use” data)
`Conditions for Use` are typically applied in order to comply with the terms under which the data were collected or with other human subjects regulations. In Synapse, data that carries `Conditions for Use` is labeled as **Controlled Use**. Examples of Controlled Use data include:
*Data whose nature confers more than minimal risks of re-identification to the research participant.
*Genetic sequence or genotype data from living individuals
*Data from “vulnerable” populations as defined using OHRP guidelines
*Data generated with `Conditions for Use` as outlined in informed consents or legal agreements


### Examples of Conditions for Use
`Conditions for Use` vary broadly. Some examples include:
* Specification of what type of research or analysis can be conducted on the data, for example, a data set may only be able to be used for breast cancer research
* Specification of who can conduct research with the data set, for example, only researchers at non-profit institutions can use the data for research
* Specification that results be shared with the originating researcher/entity
* Requirement that the researcher submit an Intended Data Use statement prior to accessing the data. Note that Intended Data Use statements must be updated anytime the research plan changes.
* Additionally, use of certain data may require independent review and monitoring of research by an accredited IRB/Ethics committee. This ensures that use of data meets all applicable human subjects research regulations.

###How to set Conditions for Use?
To set `Conditions for Use` on a project, folder, file or table please contact the Synapse Access and Compliance Team (ACT) at act@synapse.org. The ACT will reach out to you to assist in setting the appropriate Conditions for Use for your content.
You can also directly add a new file or folder to a project with the desired Conditions for Use since your file will inherit the Conditions for Use of the parent folder by default. Likewise, if you add a folder, file or table to a project that has Conditions for Use, your content will inherit the Conditions for Use of that parent project. You can set local Conditions for Use for your folder, file or table but only IN ADDITION TO the existing parent project/folder’s Conditions for Use. In other words, every folder, file or table has Conditions for Use of its parent project/folder, and may have additional local Conditions for Use as needed You cannot create a folder, file or table that has fewer Conditions for Use than its parent project/folder, or that has `Conditions for Use` that conflict with the `Conditions for Use` of the parent project/file.
