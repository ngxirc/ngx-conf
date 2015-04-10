Nginx Configuration Tool (ngx-conf)
===================================

A tool to help manage nginx configuration files.

Synopsis
--------

ngx-conf [-h] [-f] [-r] [-v] {enable|disable|remove} NAME..
ngx-conf [-h] [-f] [-v] list

Description
-----------

Ngx-conf is a relatively simple tool to help manage Nginx configuration files.
It can be used to enable, disable, remove, and list configuration files. In the
case of configuration files in conf.d/\*.conf, it will handle renaming files to
an enabled/disabled state. In sites-{enabled,available}/\*, it will handle the
creation and removal of symbolic links.

Options:

**-h, --help**
  show a help message and exit
**-f, --force**
  force change, even if doing so will destroy data
**-r, --reload**
  reload configuration after change
**-v, --verbose**
  show verbose output; default is quiet unless errors

Actions:

**enable**
  enable one or more sites by name
**disable**
  disable one or more sites by name
**remove**
  remove one or more sites by name; will prompt without **-f**
**list**
  list all available site configuration files

**NAME**
  a list of configuration files to update

Using --force has the following effects:

* For the remove action, it will not prompt you to delete the file(s).
* For the enable action, it will ignore conflicts (overwrite existing files with
  a symlink).
* For the disable action, it will ignore conflicts (besides symlinks, remove
  files too).
* For the disable action, it will also delete files from sites-enabled.

Examples
--------

ngx-conf enable site1 site2 site3
  enable "site{1,2,3}" configurations
ngx-conf disable -r site
  disable "site" configuration and reload nginx
ngx-conf -f remove -r site1 site2
  remove "site{1,2}" configurations without prompting and reload nginx

Configuration Files
-------------------

Three configuration files, if present, will be read. They will be read in the
following order; the next read file will always override the previous.

1. /etc/nginx/ngx.cfg
#. /etc/ngx.cfg
#. ~/.ngx.cfg

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

Aliases
-------

If you're interested in any sort of a2{dis,en}{conf,mod,site}, you can create
some nice aliases. Examples:

* a2ensite -- alias ngxensite='ngx-conf enable'
* a2enconf -- alias ngxenconf='ngx-conf enable'
* a2dissite -- alias ngxdissite='ngx-conf disable'
* a2disconf -- alias ngxdisconf='ngx-conf disable'

Bugs
----

If you experience bugs, the best way to report them is to the upstream bug
tracker. This can be found at https://github.com/ngx/ngx-conf.

Authors
-------

The ngx-conf tool and manual page were written by Michael Lustfield <michael@lustfield.net>.
