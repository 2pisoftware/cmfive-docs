---
title: Emails
layout: page
type: tute
---

## Introduction

Cmfive supports two different types of email transports to best suit your needs.

- The <b>AWS Transport</b> uses various AWS services to make sending email faster and more reliable. <b>Note</b>, to enable the AWS Transport uploads must also stored in S3. See the uploads <ins>[tutorial](/tutorials/additional-configuration/uploads)</ins> for setup.
- The <b>SwiftMailer</b> transport uses the SwiftMailer library.

## AWS Transport

1. Add the following entries into the <b>config.php</b> file in the root directory of your Cmfive project.
```php
Config::append("email", [
    "layer" => "aws",
]);
Config::set("admin.mail.aws", [
   "queue_url" => "SQS_QUEUE_URL",
   "region"    => "SQS_QUEUE_REGION",
]);
```
2. If you're developing on Cmfive locally, also add the following. <b>Note</b>, when system.environment is set to production <ins>[AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)</ins> must be used to authenticate with AWS as this is best practice for security.
```php
Config::set("admin.mail.aws.credentials", [
    "key"    => "IAM_KEY",
    "secret" => "IAM_SECRET",
]);
Config::set("system.environment", "development");
```
3. Replace <b>SQS_QUEUE_URL</b> and <b>SQS_QUEUE_REGION</b> with their respective values as well as <b>IAM_KEY</b> and <b>IAM_SECRET</b> if system.environment is set to development.
4. Make sure to clear your config cache to apply your changes.
5. Clone the Cmfive-Mail-Service-CDK <ins>[repository](https://github.com/2pisoftware/Cmfive-Mail-Service-CDK)</ins> and follow the steps outlined in the README.md file to deploy the CDK stack.

## SwiftMailer Transport

1. Add the following entries into the <b>config.php</b> file in the root directory of your Cmfive project.
```php
Config::append("email", [
    "layer"    => "smtp",
    "command"  => "",
    "host"     => "EMAIL_HOST",
    "port"     => PORT_NUMBER,
    "auth"     => true,
    "username" => "EMAIL_USERNAME",
    "password" => "EMAIL_PASSWORD",
]);
```
2. Replace <b>EMAIL_HOST</b>, <b>PORT_NUMBER</b>, <b>EMAIL_USERNAME</b> and <b>EMAIL_PASSWORD</b> with their respective values.
3. Make sure to clear your config cache to apply your changes.