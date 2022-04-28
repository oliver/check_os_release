# check_os_release #

This is a Nagios/Icinga plugin to check if the currently installed operating system version is outdated. It checks whether the installed version is about to reach end-of-life or whether a newer release is available.

Currently only Debian and Ubuntu are thoroughly supported. Experimental support
for Red Hat Linux derivatives has been added.

Information about releases and end-of-life dates is retrieved from https://salsa.debian.org/debian/distro-info-data/ or (if `--localDID` is specified) from the /usr/share/distro-info directory, which is provided by the distro-info-data package.

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

## Requirements

* Python 3
* internet access (to download the latest release data); or a local up-to-date installation of distro-info-data package (specify `--localDID` parameter to use this)

### Debian/Ubuntu notes

When a distribution version goes EOL the "distro-info-data" package stops being
updated, so while it may well have the EOL date and warn about this version
being EOL the feature to tell you the latest version will not work.

### RedHat/CentOS/Fedora notes

The packages required to get this to work with older releases that do not have
python3 etc by default seem to be python3 and redhat-lsb (or maybe their 
dependencies). Also, if you use it, watch out for SELinux labelling, compare
with other plugins if odd access issues ensue.

They stopped using codenames for their releases some time ago, which meant some
extra code to cope with this while Debian derived distributions continue to do
so.

RH does not seem to provide any dynamic feed for their EOL version data, so only
local csv files will work ("--localDID"). This carries a maintenance overhead 
that the authors do not want long term, so we are hoping for volunteers to
update the relevant CSV files when new releases come out. The format is easy. 
By the way the code will not explicitly stop you using non-local CSV files, in
case you wanted to centralise the data, or RH ever do start running such data
feeds in future (or if we just missed them!).

Because RH also does not seem to provide a package like 'distro-info-data' the
files need to be added into /usr/share/distro-info/ manually, or with a config
management system like ansible. Some playbooks et al for this may be added
later.

The one-off examples to get this working at a point in time (only very lightly
tested and checked) are in the rh-distro-info directory. Their content has been
sourced from pages on the very excellent Wikipedia.
