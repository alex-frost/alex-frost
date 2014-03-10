---
layout: post
title:  "Postgres install on Debian Jessie"
date:   2014-03-05 21:01:16
categories: postgres postgresql debian jessie
---
Heroku only uses postgresql and this was the first reason I wanted it installed.

In Debian Jessie I needed to

`apt-get install postgresql postgresql-contrib`

(without the postgresql-contrib package I got `PG::UndefinedFile: ERROR:  could not open extension control file "/usr/share/postgresql/9.3/extension/hstore.control": No such file or directory
: CREATE EXTENSION IF NOT EXISTS "hstore"`).
Then I needed to add a super-user to the db:
`sudo -u postgres createuser <YOUR.USERNAME> -s`

The defaults in Debian Jessie postgresql are set to be secure.  This is great if
you are serving something in the scary internet world but if you are developing
locally on a single login machine its a bit of a pain as it won't work if your
superuser has no password. I edited my `/etc/postgresql/9.3/main/pg_hba.conf` to
use the `trust` instead of the `md5` connection method, e.g.

```
# TYPE  DATABASE        USER            ADDRESS                 METHOD

# "local" is for Unix domain socket connections only
local   all             all                                     trust
```

Then restarted postgres ``/etc/init.d/postgresql restart`` and off I went to get the pg gem...
