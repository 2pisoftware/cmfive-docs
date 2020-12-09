---
title: Uploads
layout: page
type: tute
---

## Introduction

Cmfive supports two different types of file adapters for uploads to best suit your needs.

- The <b>Local Adapter</b> is enabled by default and requires no further setup.
- The <b>S3 Adapter</b> provides a more available and reliable solution.

## S3 Adapter

1. Add the following entries into the <b>config.php</b> file in the root directory of your Cmfive project.
```php
Config::set("file.adapters.local.active", false);
Config::set("file.adapters.s3", [
   "active"      => true,
   "region"      => "S3_BUCKET_REGION",
   "version"     => "2006-03-01",
   "credentials" => [
       "key"    => "IAM_KEY",
       "secret" => "IAM_SECRET",
   ],
   "bucket"      => "S3_BUCKET_NAME",
   "options"     => [
       "directory" => "uploads",
       "create"    => true
   ],
]);
```
2. If you're developing on Cmfive locally, also add the following. <b>Note</b>, when system.environment is set to production <ins>[AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)</ins> must be used to authenticate with AWS as this is best practice for security.
```php
Config::set("file.adapters.s3.credentials", [
    "key"    => "IAM_KEY",
    "secret" => "IAM_SECRET",
]);
Config::set("system.environment", "development");
```
3. Replace <b>S3_BUCKET_REGION</b>, <b>IAM_KEY</b>, <b>IAM_SECRET</b> and <b>S3_BUCKET_NAME</b> with their respective values as well as <b>IAM_KEY</b> and <b>IAM_SECRET</b> if system.environment is set to development.
4. Make sure to clear your config cache to apply your changes.
5. If you have any files stored locally from prior to using the S3 Adapter you can run <b>file transfer tool</b> in the admin module from within Cmfive to move them to S3.
![File Transfer Tool](/assets/images/file_transfer_tool.png)