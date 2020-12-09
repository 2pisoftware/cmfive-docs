---
title: Cmfive Test Framework
layout: page
type: doc
---

## Install Codeception

This guide assumes Cmfive is installed, by cloning or downloading [the Boilerplate repository](https://github.com/2pisoftware/cmfive-boilerplate) into a directory of your choosing. (See: [Installation](/documentation/installation)) Additional PHP libraries for Codeception are  independent of Cmfive, using Composer locally. But note: the DOM XML extension for PHP needs to be enabled for Codeception to function. Please check your PHP language settings for this.

To set up Codeception, first download and unpack a current version of composer.phar into your folder:
```batch
cmfive-boilerplate/test/Codeception
```

Then, from within that folder, execute:
```batch
php ./composer.phar require codeception/codeception --dev

```
You should now see Codeception and all libraries have been installed to:
```batch
cmfive-boilerplate/test/Codeception/vendor/
```

Finally, in bash, execute:
```batch
vendor/bin/codecept bootstrap
```
Or, for Windows:
```batch
vendor\bin\codecept.bat bootstrap
```

This will set up all the placeholder file structures Cmfive uses to assemble test suites from modules.