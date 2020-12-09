---
title: Cmfive Test Framework
layout: page
type: doc
---

## Introduction

Cmfive boilerplate provisions Cmfive's test framework.
The framework:
 - is built in PHP on Codeception with Selenium
 - is supported by Cmfive CLI tools
 - encourages acceptance testing during module development
 - allows modular test functions to be shared
 - offers base functions for Cmfive UI and data CRUD
 - avoids reliance on live data or prescribed Cmfive configurations

The test framework is powerful and should not be enabled in live or production environments! To do so suggests untested features are being released, and risks allowing unaware users to corrupt data by running tests inappropriately. Also, the Codeception and Selenium resources are provisioned independently of Cmfive's PHP requirements so should not need to be present on a production server.