---
title: Report
layout: page
type: doc
---

## Introduction

The report module allows users to write custom MYSQL reports that can be saved and run when needed.

## Setup

1. Before you learn how to use reports you'll need to make sure your config is setup correctly. Add the following entries into the <b>config.php</b> file in the root directory of your Cmfive project.
```php
Config::set("report.database", [
    "hostname"  => "DB_HOSTNAME",
    "username"  => "DB_USERNAME",
    "password"  => "DB_PASSWORD",
    "database"  => "DB_NAME",
    "driver"    => "mysql"
]);
```
2. Replace <b>DB_HOSTNAME</b>, <b>DB_USERNAME</b>, <b>DB_PASSWORD</b> and <b>DB_NAME</b> with their respective values.
3. To clear your config cache to apply your changes.

## Writing Reports

## Running Reports