---
layout: post
title: "S3cmd: Frequently Used Commands"
excerpt: "I’ve found S3cmd to be a great tool for interacting with S3 on AWS.  S3cmd is written in Python, is open source, and is free even for commercial use."
tags: [Cloud, Data]
comments: true
---

Before I discovered [S3cmd](http://s3tools.org/s3cmd), I had been using the [S3 console](http://aws.amazon.com/console/) to do basic operations and [boto](https://boto.readthedocs.org/en/latest/) to do more of the heavy lifting.  However, sometimes I just want to hack away at a command line to do my work.

##### S3cmd

I've found S3cmd to be a great command line tool for interacting with S3 on AWS.  S3cmd is written in Python, is open source, and is free even for commercial use.  It offers more advanced features than those found in the [AWS CLI](http://aws.amazon.com/cli/)

##### Configuring S3cmd

Running the following command will prompt you to enter your AWS access and AWS secret keys. To follow security best practices, make sure you are using an IAM account as opposed to using the root account.

{% highlight bash %}
s3cmd --configure
{% endhighlight %}

I also suggest enabling GPG encryption which will encrypt your data at rest, and enabling HTTPS to encrypt your data in transit.

##### Frequently Used Commands

{% highlight bash %}
# List all buckets
s3cmd ls

# List the contents of the bucket
s3cmd ls s3://my-bucket-name

# Upload a file into the bucket (private)
s3cmd put myfile.txt s3://my-bucket-name/myfile.txt

# Upload a file into the bucket (public)
s3cmd put --acl-public --guess-mime-type myfile.txt s3://my-bucket-name/myfile.txt

# Recursively upload a directory to s3
s3cmd put --recursive my-local-folder-path/ s3://my-bucket-name/mydir/

# Download a file
s3cmd get s3://my-bucket-name/myfile.txt myfile.txt

# List bucket disk usage (human readable)
s3cmd du -H s3://my-bucket-name/

# Sync local (source) to s3 bucket (destination)
s3cmd sync my-local-folder-path/ s3://my-bucket-name/

# Sync s3 bucket (source) to local (destination)
s3cmd sync s3://my-bucket-name/ my-local-folder-path/

# Do a dry-run (do not perform actual sync, but get information about what would happen)
s3cmd --dry-run sync s3://my-bucket-name/ my-local-folder-path/

# Apply a standard shell wildcard include to sync s3 bucket (source) to local (destination)
s3cmd --include '2014-05-01*' sync s3://my-bucket-name/ my-local-folder-path/
{% endhighlight %}