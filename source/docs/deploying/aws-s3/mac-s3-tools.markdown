---
layout: page
title: "Installing Amazon S3 Tools"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/deploying/aws-s3/mac-s3-tools/
---
Amazon S3 Tools is a free command line tool and client for Mac OS X that enables uploading, retrieving, and managing data in Amazon S3.

## Requirements
1. Mac OS X 10.6 and above  
2. [GPG tools suite](https://gpgtools.org/gpgsuite.html){:target="_new"} 
3. [Amazon AWS S3 account](http://aws.amazon.com/s3/){:target="_new"}

## Step 1
You will need your Amazon AWS security credentials. First, log into your Amazon AWS account. Then, navigate to [Security Credentials](https://console.aws.amazon.com/iam/home#security_credential){:target="_new"}.

![AWS Nav Menu - Security Credentials](/images/docs/AWS_navmenu_securcred.png)

Expand the menu `Access Keys (Access Key ID and Secret Access Key)` and select `Create New Access Key`

![AWS Security Credentials Page](/images/docs/AWS_securcred_page.png)

Select `Download Key File` and save the downloaded file `rootkey.csv` someplace you can easily access for the next step.

## Step 2
There are two ways to download and install Amazon S3 Tools (s3cmd): download from [source](http://s3tools.org/download){:target="_new"} or via the [Homebrew](brew.sh){:target="_new"} package manager.

As far as I know, Homebrew's installation of Amazon S3 Tools does not support the Amazon CloudFront cache invalidation option. If that's important to you, download and install from source. If you don't know what cache invalidation means, I recommend you use Homebrew package manager.

### Downloads
**Source:** [s3cmd.org](http://s3tools.org/download){:target="_new"}    
{% raw %}- or - {% endraw %}  
**Homebrew:** [brew.sh](brew.sh){:target="_new"}  
After install, run `$ brew install s3cmd`

## Step 3
Install [GPG Tools Suite](https://gpgtools.org/gpgsuite.html){:target="_new"} if you haven't already.

Run `$ s3cmd --configure`

You will be prompted to enter five pieces of information:

~~~bash
Access Key:
Secret Key:
Default Region:
Path to GPG program:
Default output format:
~~~

`Access Key:` Enter the access key from the `rootkey.csv` file that you downloaded in Step 1.

`Secret Key:` Enter the secret key from the `rootkey.csv` file that you downloaded in Step 1.

`Default Region:` Choose the region closest to you from the list of [AWS Regions](http://docs.aws.amazon.com/ElasticMapReduce/latest/DeveloperGuide/emr-plan-region.html).

`Path to GPG program:` Open a new terminal session and run `$ which gpg`. Copy the path that's returned, then go back to the s3cmd configuration wizard and paste the path.

`Default output format:` Default output format can be either json, text, or table. If you don't specify an output format, json will be used.

**Example**

The keys below are invalid and for demonstration purposes only.

~~~bash
$ s3cmd --configure

Enter new values or accept defaults in brackets with Enter.  
Refer to user manual for detailed description of all options.

Access key and Secret key are your identifiers for Amazon S3  
Access Key: AKIAI44QH8DHBEXAMPLE
Secret Key: je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
Default Region: us-east-1

Encryption password is used to protect your files from reading  
by unauthorized persons while in transfer to S3  
Encryption password: make-your-own-password  
Path to GPG program: /usr/local/bin/gpg

When using secure HTTPS protocol all communication with Amazon S3  
servers is protected from 3rd party eavesdropping. This method is  
slower than plain HTTP and can't be used if you're behind a proxy  
Use HTTPS protocol [No]: yes

New settings:  
  Access Key: AKIAI44QH8DHBEXAMPLE
  Secret Key: je7MtGbClwBF/2Zp9Utk/h3yCo8nvbEXAMPLEKEY
  Encryption password: make-your-own-password
  Path to GPG program: /usr/local/bin/gpg
  Use HTTPS protocol: True
  HTTP Proxy server name:
  HTTP Proxy server port: 0

Test access with supplied credentials? [Y/n] y  
Please wait, attempting to list all buckets...  
Success. Your access key and secret key worked fine :-)

Now verifying that encryption works...  
Success. Encryption and decryption worked fine :-)

Save settings? [y/N] y  
Configuration saved to '/Users/your-account/.s3cfg'
~~~

If everything went well, you can continue setting up [Deployment with Amazon AWS S3](/docs/deploying/aws-s3/)
