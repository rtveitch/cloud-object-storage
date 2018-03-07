---

copyright:
  years: 2017
lastupdated: "2018-03-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}

# Uploading data

After getting your buckets organized it's time to add some objects.  Depending on how you want to use your storage, there are different ways to get data into the system. A data scientist might have a small number of very large files that will be used for analytics, a systems administrator might need to keep database backups in sync with local files, and a developer could be writing software that needs to read and write millions of files. Each of these scenarios will likely want to use different methods for data ingest.

## Using the console

Typically, using the web-based console is not the most common way to use {{site.data.keyword.cos_short}}.  Objects are limited to 200MB in size and the file name and key will be identical.  Multiple objects can be uploaded at the same time, and if the browser allows for multiple threads each object will be uploaded using multiple parts in parallel. Support for larger object sizes and improved performance (depending on network factors) is provided via the Aspera plugin for High-Speed Transfer.

### Using High-Speed Transfer
{: #high-speed-transfer}

When uploading an object using the console, the dialog box will present the option of using High-Speed Transfer.  Instead of the typical HTTP `PUT`, this option uploads the object using the [FASP protocol](http://asperasoft.com/technology/transport/fasp/) from [IBM Aspera](https://www.ibm.com/cloud/high-speed-data-transfer). Click the **Download plugin** link and you'll be prompted to install the Aspera plugin for your web browser.

After the plugin is installed, it's possible to set High-Speed Transfer as the default for any uploads to the target bucket using the same browser by checking the box labeled **Remember my browser preferences**.  There are also toggle switches available in the bucket configuration page under "Transfer options" that allow you to set different defaults for uploads and downloads.

## Using a compatible tool

Some users will want to use some sort of standalone utility to interact with their storage.  As the COS API supports the most common set of S3 API operations, many S3-compatible tools can also connect to {{site.data.keyword.cos_short}} using [HMAC credentials](/docs/services/cloud-object-storage/hmac/credentials.html).

Some examples include file explorers like [Cyberduck](https://cyberduck.io/) or [Transmit](https://panic.com/transmit/), backup utilities like [Cloudberry](https://www.cloudberrylab.com/) and [Duplicati](https://www.duplicati.com/), command line utilities like [s3cmd](https://github.com/s3tools/s3cmd) or [Minio Client](https://github.com/minio/mc), and many others.

## Using the API

Most programmatic applications of object storage will use an SDK (such as [Java](/docs/services/cloud-object-storage/libraries/java.html), [node.js](/docs/services/cloud-object-storage/libraries/node.html), or [Python](/docs/services/cloud-object-storage/libraries/python.html)) or the [COS API](/docs/services/cloud-object-storage/api-reference/about-compatibility-api.html). Typically objects will be uploaded in [multiple parts](/docs/services/cloud-object-storage/basics/multipart.html), with part size and number of parts configured by a Transfer Manager class.  