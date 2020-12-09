---
title: Logs
layout: page
type: tute
---

## Introduction

Cmfive supports two different types of log targets to best suit your needs.

- The <b>AWS Target</b> provides a more reliable solution with the option to specify a retention period (in days).
- The <b>File Target</b> is enabled by default and requires no further setup.

## AWS Target

1. Add the following entries into the <b>config.php</b> file in the root directory of your Cmfive project.
```php
Config::set("admin.logging", [
        "target"           => "aws",
        "retention_period" => RETENTION_PERIOD,
        "cloudwatch"       => [
            "group_name"      => "GROUP_NAME",
            "stream_name_app" => "APP_NAME",
            "region"          => "CLOUDWATCH_REGION",
            "version"         => "latest",
        ]
]);
```
2. If you're developing on Cmfive locally, also add the following. <b>Note</b>, when system.environment is set to production <ins>[AWS IAM Roles](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html)</ins> must be used to authenticate with AWS as this is best practice for security.
```php
Config::set("admin.logging.cloudwatch.credentials", [
    "key"    => "IAM_KEY",
    "secret" => "IAM_SECRET",
]);
Config::set("system.environment", "development");
```
3. Replace <b>RETENTION_PERIOD</b>, <b>GROUP_NAME</b>, <b>APP_NAME</b>, <b>CLOUDWATCH_REGION</b> with their respective values as well as <b>IAM_KEY</b> and <b>IAM_SECRET</b> if system.environment is set to development.
4. Make sure to clear your config cache to apply your changes.