---
title: Can't Connect to Database Error
layout: page
type: tute
---

## Can't Connect to Database Error in Terminal

<!--known issue to be fixed-->
<!--go to logs to find ip address. See Cmfive Logs to find logs-->
To find your log files in cmfive go to /storage/log. Each log file has "cmfive", a date, and is appended with ".log". Scroll to the bottom of the log folder. The last file will have todays date on it.<br>
The log files are automatically created as you use the database and record the pages that each user visits, and any arrors that pop-up. The most recent log is always at the bottom of the log folder, so it is the one you will use when trouble shooting.

<!--attach shell to mysql database-->
Go to the Docker tab on the left of VSCode. it looks like this.

![Docker tab](/assets/images/docker.png)

Right click on the database container that satrts with mysql. Choose attach a shell. You can now type in its shell terminal using the terminal at the bottom of the VSCode window.

<!--Create user called cmfive @ ip address. Grant all privileges to cmfive.* to new user with ip address-->
```bash
FLUSH PRIVILEGES;
```

Please note, this is only a temporary fix and will need to be repeated each time you start a session, as the IP address changes.