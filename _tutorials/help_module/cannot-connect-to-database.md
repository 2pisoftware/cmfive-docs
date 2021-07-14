---
title: Can't Connect to Database Error
layout: page
type: tute
---

## Can't Connect to Database Error in Terminal

<!--known issue to be fixed-->
<!--go to logs to find ip address. See Cmfive Logs to find logs-->
<!--attach shell to mysql database-->
<!--Create user called cmfive @ ip address. Grant all privileges to cmfive.* to new user with ip address-->
```bash
FLUSH PRIVILEGES;
```

Please note, this is only a temporary fix and will need to be repeated each time you start a session, as the IP address changes.