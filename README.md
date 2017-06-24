# check_os_release #

This is a Nagios/Icinga plugin to check if the currently installed operating system version is outdated. It checks whether the installed version is about to reach end-of-life or whether a newer release is available.

Currently only Debian and Ubuntu are supported.

## Usage ##
```
check_os_release -h
usage: check_os_release [-h] [--eolWarningDays DAYS] [--eolCriticalDays DAYS]
                        [--releaseWarningDays DAYS]
                        [--releaseCriticalDays DAYS] [--lts] [--server]

Check whether OS release is outdated.

optional arguments:
  -h, --help            show this help message and exit
  --eolWarningDays DAYS
                        set WARNING status if less than DAYS until end-of-life
  --eolCriticalDays DAYS
                        set CRITICAL status if less than DAYS until end-of-
                        life
  --releaseWarningDays DAYS
                        set WARNING status if new release available for more
                        than DAYS
  --releaseCriticalDays DAYS
                        set CRITICAL status if new release available for more
                        than DAYS
  --lts                 [Ubuntu] check only for LTS releases
  --server              [Ubuntu] check for server EOL dates
```
