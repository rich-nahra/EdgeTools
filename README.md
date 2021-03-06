# EdgeTools
Tools for working with Apigee Edge

## Before you Start....

A note about enabling Drupal's REST Services...

Some of the tools in this repo invoke Administrative REST APIs on Apigee Edge.  Some of the tools in this repo invoke REST APIs exposed by Drupal to perform various operations, like creating new users, deleting and creating new portal content, new FAQs, and so on. For the tools that invoke REST APIs on Drupal, all of the operations require the REST services to be enabled in Drupal.

[This blog post](https://www.dinochiesa.net/?p=1297) describes in some detail the how and why of setting up REST access into Drupal 7.

In summary, though, you need to do these things as an administrator for Drupal:

1. In Admin / Modules, enable the "REST Server" (rest_server) module. It will already be installed as part of the Apigee Edge developer portal. 

2. In Admin / Structure / Services, add an endpoint for REST services.  Use values: rest REST and /rest. Enable "Session Authentication"

3. In the subsequent page, click "Edit Resources" and tick the boxes to enable node, system, taxonomy_term, taxonomy_vocabulary, and user. 



## Provision DevPortal Users

[This script creates dev portal users](provisionDevPortalUsers/provisionDevPortalUsers.js) by invoking the REST API on Drupal. 

In order to use this script, you need to have enabled the REST Services module in Drupal, and you need to have exposed the rest endpoint on the /rest uri path. Also, the users resource must be available there.

You supply the list of users to create in a .csv file. An example is provided. 
After running the script, new users will be provisioned in the devportal, and the corresponding Developers will be created in Edge.



## Activate DevPortal Users

[This script lists and optionally activates all non-activated dev portal users](activateDevPortalUsers/activateDevPortalUsers.js) by invoking the REST API on Drupal. 

In order to use this script, you need to have enabled the REST Services module in Drupal, and you need to have exposed the rest endpoint on the /rest uri path. Also, the users resource must be available there.

After running the script, all users will have been activated.



## Load DevPortal Content

[This script loads devportal content](loadDevPortalContent/loadDevPortalContent.js) by invoking the REST API on Drupal. 

In order to use this script, you need to have enabled the REST Services module in Drupal, and you need to have exposed the rest endpoint on the /rest uri path. Also, the users resource must be available there.

You specify the content in a specially-formatted JSON file.  An [example](loadDevPortalContent/portalcontent.json) is provided. Warning: this script will delete data. It will remove existing FAQs and Forum postings. It is suitable for use after initially deploying your dev portal, when all of the content is "lorem ipsum" text.

After running the script, all new content will be available.



## Bulk Export APIs

[This tool](bulkExportApis) exports all API proxies in an Edge organization. 


## Find API Key

Given an API Key, [the findApiKey tool](findApiKey) finds which Developer App it belongs to. 


## Find API Product for Proxy

Given an API Proxy, [the findApiProductForProxy tool](findApiProductForProxy) will find any API Product that contains it.



## API Proxy Diff

[This tool](diffApiProxyRevisions) downloads 2 revisions of an API Proxy from Edge, and
performs a diff on them. 


## BaaS Loader + Exporter

[This set of scripts](baasLoadExport) helps do three things:

* load items into a BaaS/Usergrid collection
* exports items from a BaaS/Usergrid collection into a file
* deletes all items from a BaaS/Usergrid collection


## New Keystore

[The newKeystore tool](newKeystore) creates a JAR and imports it into a new [Keystore](http://docs.apigee.com/api-services/content/keystores-and-truststores).
Also creates a new keystore Reference (a magical type of thing that is not documented by Apigee at this moment). This tool is handy
when updating certs that will expire, as documented [here](http://docs.apigee.com/api-services/content/keystores-and-truststores#createakeystore).

Using keystores and references for your vhosts applies only when the TLS terminates at
the Edge routers.  If you are using a hosted Apigee Edge organization, your TLS may
terminate at a load balancer.  In which case, this tool does not apply, and you should
contact Apigee Support directly.


## Find KVM Access

The [findKvmAccess](findKvmAccess) tool examines all the API proxies in an Edge organization, for policies that access the KVM.  It reports the matching policies .



# Notes

These tools are built in nodejs, and in bash. 

# License

This material is Copyright 2015-2016 Apigee Corporation, 
and Copyright 2016 Google, Inc.
and is licensed under the Apache 2.0 license. See the [LICENSE](LICENSE) file. 

