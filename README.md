# check_os_release #

This is a Nagios/Icinga plugin to check if the currently installed operating system version is outdated. It checks:
- whether the installed version is about to reach end-of-life (see `--eolWarningDays`, `--eolCriticalDays`, `--eolIgnore` parameters),
- or whether a newer release is available (see `--releaseWarningDays`, `--releaseCriticalDays`, `--releaseIgnore` parameters).

Currently only Debian and Ubuntu are supported.

Information about releases and end-of-life dates is retrieved from https://salsa.debian.org/debian/distro-info-data/ or (if `--localDID` is specified) from the /usr/share/distro-info directory, which is provided by the distro-info-data package.

## Requirements

* Python 3
* internet access (to download the latest release data); or a local up-to-date installation of distro-info-data package (specify `--localDID` parameter to use this)


## Usage ##
```
usage: check_os_release [-h] [-v] [--eolWarningDays DAYS]
                        [--eolCriticalDays DAYS] [--eolIgnore]
                        [--releaseWarningDays DAYS]
                        [--releaseCriticalDays DAYS] [--releaseIgnore] [--lts]
                        [--server] [--cacheDir CACHEDIR]
                        [--cacheExpiration DAYS] [--localDID]

Check whether OS release is outdated.

optional arguments:
  -h, --help            show this help message and exit
  -v, --verbose         increase output verbosity
  --eolWarningDays DAYS
                        set WARNING status if less than DAYS until end-of-life
                        (default: 30)
  --eolCriticalDays DAYS
                        set CRITICAL status if less than DAYS until end-of-
                        life (default: 7)
  --eolIgnore           ignore end-of-life
  --releaseWarningDays DAYS
                        set WARNING status if new release available for more
                        than DAYS (default: 0)
  --releaseCriticalDays DAYS
                        set CRITICAL status if new release available for more
                        than DAYS (default: 30)
  --releaseIgnore       ignore any new release
  --lts                 [Ubuntu] check only for LTS releases
  --server              [Ubuntu] check for server EOL dates
  --cacheDir CACHEDIR   optional directory where data files should be cached
                        (default: no caching)
  --cacheExpiration DAYS
                        for how many days should data files be cached
                        (default: 7)
  --localDID            use local distro-info-data, from /usr/share/distro-
                        info
```
