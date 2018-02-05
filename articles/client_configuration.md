---
title: Client Configuration
layout: article
excerpt: How to fine-tune your config file.
category: howto
---

# Overview

The programmatic clients in Synapse can use a configuration file (called `.synapseConfig`) that can store frequently used client-interactions. The most commonly used example is storing your login credentials for quick and easy authentication when using the programmatic clients. However, this config file can take many more parameters, such as:

- specifying a new cache location
- add credentials to access files stored outside of Synapse storage (e.g. SFTP, AWS-S3, etc.)


# Example Config File

The code block below displays an example config file with the available parameters commented out. This file should be named `.synapseConfig` and saved to your home directory. Please note the period at the beginning of the file which makes this a hidden, system file on Linux-like OS's since it will contain sensitive information.

```bash
###########################
# Login Credentials       #
###########################
 
## Used for logging in to Synapse
## you may also specify an apikey instead of password. If both password and apikey are specified, the apikey is ignored
## Alternatively you can use rememberMe=True in synapseclient.login or login subcommand of the commandline client to
## cache your API key elsewhere.
#[authentication]
#username = <username>
#password = <password>
#apikey = <apikey>
 
## If you have projects with file stored on SFTP servers, you can specify your credentials here
## You can specify multiple sftp credentials
#[sftp://some.sftp.url.com]
#username= <sftpuser>
#password= <sftppwd>
#[sftp://a.different.sftp.url.com]
#username= <sftpuser>
#password= <sftppwd>
 
 
## If you have projects that need to be stored in an S3-like (e.g. AWS S3, Openstack) storage but cannot allow Synapse
## to manage access your storage you may put your credentials here.
## To avoid duplicating credentials with that used by the AWS Command Line Client,
## simply put the profile name form your ~/.aws/credentials file
## more information about aws credentials can be found here http://docs.aws.amazon.com/cli/latest/userguide/cli-config-files.html
#[https://s3.amazonaws.com/bucket_name] # this is the bucket's endpoint
#profile_name=local_credential_profile_name
 
 
###########################
# Caching                 #
###########################
## your downloaded files are cached to avoid repeat downloads of the same file. change 'location' to use a different folder on your computer as the cache location
# [cache]
# location = <your cache location>
 
 
###########################
# Advanced Configurations #
###########################
 
## If this section is specified, then the synapseclient will print out debug information
# [debug]
 
## Some integration tests require a second Synapse user. This should only be necessary for developers
#[test-authentication]
#username = <username>
#password = <password>
#principalid = <userId>

```