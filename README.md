# About This Repository

**TF6760-File-Download** is a sample project for downloading files over the HTTPS/REST protocol. This can be used to retrieve files from AWS S3 Buckets and many other sources.

Services such as AWS S3 have a request limitation of 1MB per request, and downloading files >1MB over a single command is not possible. There are usually ways around this within the services environment, such as signed links for S3. However, signed links only last for a specific amount of time and are not as friendly to work with.

Instead of a single large request, this project utilizes a "chunker" to break the larger file into smaller segments. By default, the FB's constant CHUNK_SIZE is set to 1000kb to avoid going over a request limitation.

```reStructuredText
CHUNK_SIZE : ULINT := 1000*1024; //1000*1024 = 1000Kb Chunk size
```

The file download FB processes data as follows:

1. Completes HTTPS/REST request for header data only
2. Looks for the 'Accept-Ranges' and 'Content-Length' fields
3. Opens file on hard disk for writing in binary mode
4. Loops through HTTPS/REST requests of CHUNK_SIZE until 'Content-Length' is reached
5. Closes and saves file

There is also a status feedback that is fed out of the FB in the form of a structure via P_Status. It will relay if the process is complete/error/busy and also a 0-100% download progress.



This sample is created by [Beckhoff Automation LLC.](https://www.beckhoff.com/en-us/), and is provided as-is under the Zero-Clause BSD license.



# How to get support

Should you have any questions regarding the provided sample code, please contact your local Beckhoff support team. Contact information can be found on the official Beckhoff website at https://www.beckhoff.com/en-us/support/.



## Requirements

The following components must be installed to run sample code:

- [TE1000 TwinCAT 3 Engineering](https://www.beckhoff.com/en-en/products/automation/twincat/te1xxx-twincat-3-engineering/te1000.html) version 3.1.4024.50 or higher
