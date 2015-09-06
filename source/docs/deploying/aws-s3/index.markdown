---
layout: page
title: "Deploying with Amazon AWS S3"
comments: false
sharing: false
footer: false
sidebar: false
permalink: /docs/deploying/aws-s3/
---

## Set Up Amazon AWS S3
Amazon hosts static sites directly through the S3 'buckets' they provide. Create a bucket named the same as your website's domain name, formatted as **www.yourdomain.com**. If you don't include `www` in your S3 bucket name, then anyone who goes to your website with a `www` prefix will get a `404 Page Not found` error when trying to visit your site. (We will set up `yourdomain.com` to redirect visitors to `www.yourdomain.com` in a later step.)

After creating a bucket, go to `Properties`, expand the `Static Website Hosting` dropdown menu and select `Enable website hosting`. Set the `Index Document:` to "index.html".

![Amazon AWS S3 bucket properties](/images/docs/aws-bucket-properties.png)

## Set Up Deployment in Showcase

This setup uses Amazon S3 Tools to upload generated site content to the bucket on Amazon AWS S3 (see Step 1). S3 Tools is a command line program that will allow you to push the site up to Amazon using a rake task.

### Mac OS X

#### Requirements 
1. [Amazon AWS S3 account](http://aws.amazon.com/s3/){:target="_new"}
2. [Amazon S3 Tools (s3cmd)](/docs/deploying/aws-s3/mac-s3-tools) (free)

#### Update Rakefile
In your `Rakefile`, look for the `deploy_default = "rsync"` variable and change it to `"s3"`. Add a variable for your s3 bucket as well.

{% coderay Rakefile line_number_start:16 lang:ruby %}
deploy_default = "s3" # change "rsync" to "s3"
s3_bucket = "www.yourdomain.com" # add this variable underneath deploy_default
{% endcoderay %}

Add this task to the Deploying section of your `Rakefile`.

{% coderay Rakefile line_number_start:400 lang:ruby %}
##############
# Deploying  #
##############

...

desc "Deploy website via s3cmd"
task :s3 do
  exclude = ""
  if File.exists?('./s3-exclude')
    exclude = "--exclude-from \'#{File.expand_path('./s3-exclude')}\'"
  end

  puts "## Deploying website via s3cmd"
  ok_failed system("s3cmd sync --acl-public --reduced-redundancy #{exclude} --delete-removed #{public_dir}/* s3://#{s3_bucket}/")
end
{% endcoderay %}

### Windows

#### Requirements 
1. [Amazon AWS S3 account](http://aws.amazon.com/s3/){:target="_new"}
2. [S3Express](http://www.s3express.com/download.htm) ($99)  
- If you have deployed Jekyll, Octopress or Showcase to Amazon S3 from a Windows machine using free tools, help out the community by shooting me an email.

#### Update Rakefile
In your `Rakefile`, look for the `deploy_default = "rsync"` variable and change it to `"s3"`. Add a variable for your s3 bucket as well.

{% coderay Rakefile line_number_start:16 lang:ruby %}
deploy_default = "s3" # change "rsync" to "s3"
s3_bucket = "www.yourdomain.com" # add this variable underneath deploy_default
{% endcoderay %}

Add this task to the Deploying section of your `Rakefile`.  
(**Note:** I am a Mac user. I wrote this rake task based on the S3Express documentation, but I have not tested on a Windows machine.)

{% coderay Rakefile line_number_start:400 lang:ruby %}
##############
# Deploying  #
##############

...

desc "Deploy website via s3cmd"
task :s3 do
  exclude = ""
  if File.exists?('.\s3-exclude')
    exclude = "-exclude:\'#{File.expand_path('.\s3-exclude')}\'"
  end

  puts "## Deploying website via s3cmd"
  ok_failed system("s3express put #{exclude} -cacl:public-read -rr -purge #{public_dir}\ s3://#{s3_bucket}/")
end
{% endcoderay %}

### Deploy!
You must have [Amazon S3 Tools (Mac)](/docs/deploying/aws-s3/mac-s3-tools) or [S3Express (Windows)](http://www.s3express.com/download.htm) downloaded, installed, and configured for the rake task to work. If you have not already done so, set those up and then come back.

~~~bash
$ bundle exec rake generate
$ bundle exec rake deploy
~~~

Your files should now be pushed up to your Amazon S3 bucket and you should be able to view your site by visiting the **endpoint** (default URL) that was defined for your bucket, e.g. `bucketname.s3-website-us-east-1.amazonaws.com`. You can find your endpoint under bucket `Properties`. 

## Use Custom Domain with Amazon AWS S3
In this step, we will point your custom domain `www.yourdomain.com` to your site hosted on Amazon, so visitors can access your site through your domain instead of the Amazon endpoint.

### Step 1
Using your Domain Name Service (DNS) provider's tools, create a CNAME record to map `www.yourdomain.com` to your bucket's **endpoint** (under bucket `Properties`, e.g. `bucketname.s3-website-us-east-1.amazonaws.com`). The CNAME will allow visitors to access your site at `www.yourdomain.com`.

### Step 2
CNAMEs only work on subdomains like `www`, so visitors will still get an error if they visit your 'naked domain' `yourdomain.com`. An additional step is required to redirect `yourdomain.com` to `www.yourdomain.com`. Some DNS providers offer a forwarding service.

If your DNS provider doesn't, check out [WWWizer](http://wwwizer.com/naked-domain-redirect) - it's free and doesn't require registration. To use WWWizer, create an `A` / `@` record that points `yourdomain.com` to `174.129.25.170`. That's it!

**Note:** It can take anywhere from 3-72 hours for your domain to propogate (go live). **Be patient!**

## Next Steps
[Creating & Managing Portfolios](/docs/portfolios-and-projects)  
[Blogging Basics](/docs/blogging/) 
