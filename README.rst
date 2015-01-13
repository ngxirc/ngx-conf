Nginx Configuration Tool (ngx-conf)
===================================

A tool to help manage nginx confuration files.

Synopsis
--------

ngx-conf [-h] (-e ENABLE | -d DISABLE | -x REMOVE | -l) [-f] [-r] [-v]

Description
-----------

Ngx-conf is a relatively simple tool to help manage Nginx configuration files.
It can be used to enable, disable, remove, and list configuration files.

**-h, --help**
  show a help message and exit
**-e CONFIG, --enable CONFIG**
  enable a configuration file
**-d CONFIG, --disable CONFIG**
  disable a configuration file
**-x CONFIG, --remove CONFIG**
  remove a configuration file; will prompt without -f
**-l, --list**
  list configuration files
**-f, --force**
  force change, even if doing so will destroy data
**-r, --reload**
  reload configuration after change
**-v, --verbose**
  show verbose output; default is quiet unless errors

Only one action (enable|disable|edit|remove) can be performed at one time.
However, any action can be specified multiple times.

Examples
--------

* ngx -e site1 -e site2 -v -e site3
* ngx -r -d site
* ngx -f -r -x site1 -x site2

Configuration Files
-------------------

Three configuration files, if present, will be read. They will be read in the
following order; the next read file will always override the previous.

1. /etc/nginx/ngx.cfg
#. /etc/ngx.cfg
#. ngx.cfg

A sample configuration file with all options set to default::

    [DEFAULT]
    base_dir = /etc/nginx/
    conf_dir = conf.d/
    sites_en = sites-enabled/
    sites_dis = sites-available/
    conf_ext = .conf
    verbose = no
    reload = no
    force = no

Make sure that base_dir always has a trailing slash.

Any arguments given to the command will override configuration options.

Bugs
----

If you experience bugs, the best way to report them is to the upstream bug
tracker. This can be found at https://github.com/ngx/ngx-conf.

Authors
-------

This application and manual page was written by Michael Lustfield <michael@lustfield.net>.
