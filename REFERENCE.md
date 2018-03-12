# Reference

## Classes
* [`mysql::backup::mysqlbackup`](#mysqlbackupmysqlbackup): See README.me for usage.
* [`mysql::backup::mysqldump`](#mysqlbackupmysqldump): See README.me for usage.
* [`mysql::backup::xtrabackup`](#mysqlbackupxtrabackup): See README.me for usage.
* [`mysql::bindings`](#mysqlbindings): See README.md.
* [`mysql::bindings::client_dev`](#mysqlbindingsclient_dev): Private class
* [`mysql::bindings::daemon_dev`](#mysqlbindingsdaemon_dev): Private class
* [`mysql::bindings::java`](#mysqlbindingsjava): Private class
* [`mysql::bindings::perl`](#mysqlbindingsperl): Private class
* [`mysql::bindings::php`](#mysqlbindingsphp): Private class: See README.md
* [`mysql::bindings::python`](#mysqlbindingspython): Private class
* [`mysql::bindings::ruby`](#mysqlbindingsruby): Private class
* [`mysql::client`](#mysqlclient): 
* [`mysql::client::install`](#mysqlclientinstall): See README.md.
* [`mysql::params`](#mysqlparams): Private class: See README.md.
* [`mysql::server`](#mysqlserver): Class: mysql::server:  See README.md for documentation.
* [`mysql::server::account_security`](#mysqlserveraccount_security): See README.md.
* [`mysql::server::backup`](#mysqlserverbackup): See README.me for usage.
* [`mysql::server::binarylog`](#mysqlserverbinarylog): Binary log configuration requires the mysql user to be present. This must be done after package install
* [`mysql::server::config`](#mysqlserverconfig): See README.me for options.
* [`mysql::server::install`](#mysqlserverinstall): 
* [`mysql::server::installdb`](#mysqlserverinstalldb): 
* [`mysql::server::monitor`](#mysqlservermonitor): This is a helper class to add a monitoring user to the database
* [`mysql::server::mysqltuner`](#mysqlservermysqltuner): 
* [`mysql::server::providers`](#mysqlserverproviders): Convenience class to call each of the three providers with the corresponding hashes provided in mysql::server. See README.md for details.
* [`mysql::server::root_password`](#mysqlserverroot_password): 
* [`mysql::server::service`](#mysqlserverservice): 
## Defined types
* [`mysql::db`](#mysqldb): See README.md for details.
## Resource types
* [`mysql_database`](#mysql_database): Manage MySQL databases.
* [`mysql_datadir`](#mysql_datadir): Manage MySQL datadirs with mysql_install_db OR mysqld (5.7.6 and above).
* [`mysql_grant`](#mysql_grant): Manage a MySQL user's rights.
* [`mysql_plugin`](#mysql_plugin): Manage MySQL plugins.
* [`mysql_user`](#mysql_user): Manage a MySQL user. This includes management of users password as well as privileges.
## Functions
* [`mysql_deepmerge`](#mysql_deepmerge): Recursively merges two or more hashes together and returns the resulting hash.  For example:      $hash1 = {'one' => 1, 'two' => 2, 'three' =
* [`mysql_dirname`](#mysql_dirname): Returns the dirname of a path.
* [`mysql_password`](#mysql_password): Returns the mysql password hash from the clear text password.
* [`mysql_strip_hash`](#mysql_strip_hash): TEMPORARY FUNCTION: EXPIRES 2014-03-10 When given a hash this function strips out all blank entries.
## Tasks
* [`export`](#export): Allows you to backup your database to local file.
* [`sql`](#sql): Allows you to execute arbitary SQL
## Classes

### mysql::backup::mysqlbackup

See README.me for usage.


#### Parameters

The following parameters are available in the `mysql::backup::mysqlbackup` class.

##### `backupuser`

Data type: `Any`



Default value: ''

##### `backuppassword`

Data type: `Any`



Default value: ''

##### `maxallowedpacket`

Data type: `Any`



Default value: '1M'

##### `backupdir`

Data type: `Any`



Default value: ''

##### `backupdirmode`

Data type: `Any`



Default value: '0700'

##### `backupdirowner`

Data type: `Any`



Default value: 'root'

##### `backupdirgroup`

Data type: `Any`



Default value: $mysql::params::root_group

##### `backupcompress`

Data type: `Any`



Default value: `true`

##### `backuprotate`

Data type: `Any`



Default value: 30

##### `ignore_events`

Data type: `Any`



Default value: `true`

##### `delete_before_dump`

Data type: `Any`



Default value: `false`

##### `backupdatabases`

Data type: `Any`



Default value: []

##### `file_per_database`

Data type: `Any`



Default value: `false`

##### `include_triggers`

Data type: `Any`



Default value: `true`

##### `include_routines`

Data type: `Any`



Default value: `false`

##### `ensure`

Data type: `Any`



Default value: 'present'

##### `time`

Data type: `Any`



Default value: ['23', '5']

##### `prescript`

Data type: `Any`



Default value: `false`

##### `postscript`

Data type: `Any`



Default value: `false`

##### `execpath`

Data type: `Any`



Default value: '/usr/bin:/usr/sbin:/bin:/sbin'

##### `optional_args`

Data type: `Any`



Default value: []


### mysql::backup::mysqldump

See README.me for usage.


#### Parameters

The following parameters are available in the `mysql::backup::mysqldump` class.

##### `backupuser`

Data type: `Any`



Default value: ''

##### `backuppassword`

Data type: `Any`



Default value: ''

##### `backupdir`

Data type: `Any`



Default value: ''

##### `maxallowedpacket`

Data type: `Any`



Default value: '1M'

##### `backupdirmode`

Data type: `Any`



Default value: '0700'

##### `backupdirowner`

Data type: `Any`



Default value: 'root'

##### `backupdirgroup`

Data type: `Any`



Default value: $mysql::params::root_group

##### `backupcompress`

Data type: `Any`



Default value: `true`

##### `backuprotate`

Data type: `Any`



Default value: 30

##### `ignore_events`

Data type: `Any`



Default value: `true`

##### `delete_before_dump`

Data type: `Any`



Default value: `false`

##### `backupdatabases`

Data type: `Any`



Default value: []

##### `file_per_database`

Data type: `Any`



Default value: `false`

##### `include_triggers`

Data type: `Any`



Default value: `false`

##### `include_routines`

Data type: `Any`



Default value: `false`

##### `ensure`

Data type: `Any`



Default value: 'present'

##### `time`

Data type: `Any`



Default value: ['23', '5']

##### `prescript`

Data type: `Any`



Default value: `false`

##### `postscript`

Data type: `Any`



Default value: `false`

##### `execpath`

Data type: `Any`



Default value: '/usr/bin:/usr/sbin:/bin:/sbin'

##### `optional_args`

Data type: `Any`



Default value: []


### mysql::backup::xtrabackup

See README.me for usage.


#### Parameters

The following parameters are available in the `mysql::backup::xtrabackup` class.

##### `xtrabackup_package_name`

Data type: `Any`



Default value: $mysql::params::xtrabackup_package_name

##### `backupuser`

Data type: `Any`



Default value: `undef`

##### `backuppassword`

Data type: `Any`



Default value: `undef`

##### `backupdir`

Data type: `Any`



Default value: ''

##### `maxallowedpacket`

Data type: `Any`



Default value: '1M'

##### `backupmethod`

Data type: `Any`



Default value: 'mysqldump'

##### `backupdirmode`

Data type: `Any`



Default value: '0700'

##### `backupdirowner`

Data type: `Any`



Default value: 'root'

##### `backupdirgroup`

Data type: `Any`



Default value: $mysql::params::root_group

##### `backupcompress`

Data type: `Any`



Default value: `true`

##### `backuprotate`

Data type: `Any`



Default value: 30

##### `ignore_events`

Data type: `Any`



Default value: `true`

##### `delete_before_dump`

Data type: `Any`



Default value: `false`

##### `backupdatabases`

Data type: `Any`



Default value: []

##### `file_per_database`

Data type: `Any`



Default value: `false`

##### `include_triggers`

Data type: `Any`



Default value: `true`

##### `include_routines`

Data type: `Any`



Default value: `false`

##### `ensure`

Data type: `Any`



Default value: 'present'

##### `time`

Data type: `Any`



Default value: ['23', '5']

##### `prescript`

Data type: `Any`



Default value: `false`

##### `postscript`

Data type: `Any`



Default value: `false`

##### `execpath`

Data type: `Any`



Default value: '/usr/bin:/usr/sbin:/bin:/sbin'

##### `optional_args`

Data type: `Any`



Default value: []

##### `additional_cron_args`

Data type: `Any`



Default value: ''


### mysql::bindings

See README.md.


#### Parameters

The following parameters are available in the `mysql::bindings` class.

##### `install_options`

Data type: `Any`



Default value: `undef`

##### `java_enable`

Data type: `Any`



Default value: `false`

##### `perl_enable`

Data type: `Any`



Default value: `false`

##### `php_enable`

Data type: `Any`



Default value: `false`

##### `python_enable`

Data type: `Any`



Default value: `false`

##### `ruby_enable`

Data type: `Any`



Default value: `false`

##### `client_dev`

Data type: `Any`



Default value: `false`

##### `daemon_dev`

Data type: `Any`



Default value: `false`

##### `java_package_ensure`

Data type: `Any`



Default value: $mysql::params::java_package_ensure

##### `java_package_name`

Data type: `Any`



Default value: $mysql::params::java_package_name

##### `java_package_provider`

Data type: `Any`



Default value: $mysql::params::java_package_provider

##### `perl_package_ensure`

Data type: `Any`



Default value: $mysql::params::perl_package_ensure

##### `perl_package_name`

Data type: `Any`



Default value: $mysql::params::perl_package_name

##### `perl_package_provider`

Data type: `Any`



Default value: $mysql::params::perl_package_provider

##### `php_package_ensure`

Data type: `Any`



Default value: $mysql::params::php_package_ensure

##### `php_package_name`

Data type: `Any`



Default value: $mysql::params::php_package_name

##### `php_package_provider`

Data type: `Any`



Default value: $mysql::params::php_package_provider

##### `python_package_ensure`

Data type: `Any`



Default value: $mysql::params::python_package_ensure

##### `python_package_name`

Data type: `Any`



Default value: $mysql::params::python_package_name

##### `python_package_provider`

Data type: `Any`



Default value: $mysql::params::python_package_provider

##### `ruby_package_ensure`

Data type: `Any`



Default value: $mysql::params::ruby_package_ensure

##### `ruby_package_name`

Data type: `Any`



Default value: $mysql::params::ruby_package_name

##### `ruby_package_provider`

Data type: `Any`



Default value: $mysql::params::ruby_package_provider

##### `client_dev_package_ensure`

Data type: `Any`



Default value: $mysql::params::client_dev_package_ensure

##### `client_dev_package_name`

Data type: `Any`



Default value: $mysql::params::client_dev_package_name

##### `client_dev_package_provider`

Data type: `Any`



Default value: $mysql::params::client_dev_package_provider

##### `daemon_dev_package_ensure`

Data type: `Any`



Default value: $mysql::params::daemon_dev_package_ensure

##### `daemon_dev_package_name`

Data type: `Any`



Default value: $mysql::params::daemon_dev_package_name

##### `daemon_dev_package_provider`

Data type: `Any`



Default value: $mysql::params::daemon_dev_package_provider


### mysql::bindings::client_dev

Private class


### mysql::bindings::daemon_dev

Private class


### mysql::bindings::java

Private class


### mysql::bindings::perl

Private class


### mysql::bindings::php

Private class: See README.md


### mysql::bindings::python

Private class


### mysql::bindings::ruby

Private class


### mysql::client

The mysql::client class.


#### Parameters

The following parameters are available in the `mysql::client` class.

##### `bindings_enable`

Data type: `Any`



Default value: $mysql::params::bindings_enable

##### `install_options`

Data type: `Any`



Default value: `undef`

##### `package_ensure`

Data type: `Any`



Default value: $mysql::params::client_package_ensure

##### `package_manage`

Data type: `Any`



Default value: $mysql::params::client_package_manage

##### `package_name`

Data type: `Any`



Default value: $mysql::params::client_package_name


### mysql::client::install

See README.md.


### mysql::params

Private class: See README.md.


### mysql::server

Class: mysql::server:  See README.md for documentation.


#### Parameters

The following parameters are available in the `mysql::server` class.

##### `config_file`

Data type: `Any`



Default value: $mysql::params::config_file

##### `includedir`

Data type: `Any`



Default value: $mysql::params::includedir

##### `install_options`

Data type: `Any`



Default value: `undef`

##### `install_secret_file`

Data type: `Any`



Default value: $mysql::params::install_secret_file

##### `manage_config_file`

Data type: `Any`



Default value: $mysql::params::manage_config_file

##### `override_options`

Data type: `Any`



Default value: {}

##### `package_ensure`

Data type: `Any`



Default value: $mysql::params::server_package_ensure

##### `package_manage`

Data type: `Any`



Default value: $mysql::params::server_package_manage

##### `package_name`

Data type: `Any`



Default value: $mysql::params::server_package_name

##### `purge_conf_dir`

Data type: `Any`



Default value: $mysql::params::purge_conf_dir

##### `remove_default_accounts`

Data type: `Any`



Default value: `false`

##### `restart`

Data type: `Any`



Default value: $mysql::params::restart

##### `root_group`

Data type: `Any`



Default value: $mysql::params::root_group

##### `mysql_group`

Data type: `Any`



Default value: $mysql::params::mysql_group

##### `root_password`

Data type: `Any`



Default value: $mysql::params::root_password

##### `service_enabled`

Data type: `Any`



Default value: $mysql::params::server_service_enabled

##### `service_manage`

Data type: `Any`



Default value: $mysql::params::server_service_manage

##### `service_name`

Data type: `Any`



Default value: $mysql::params::server_service_name

##### `service_provider`

Data type: `Any`



Default value: $mysql::params::server_service_provider

##### `create_root_user`

Data type: `Any`



Default value: $mysql::params::create_root_user

##### `create_root_my_cnf`

Data type: `Any`



Default value: $mysql::params::create_root_my_cnf

##### `users`

Data type: `Any`



Default value: {}

##### `grants`

Data type: `Any`



Default value: {}

##### `databases`

Data type: `Any`



Default value: {}

##### `enabled`

Data type: `Any`



Default value: `undef`

##### `manage_service`

Data type: `Any`



Default value: `undef`

##### `old_root_password`

Data type: `Any`



Default value: `undef`


### mysql::server::account_security

See README.md.


### mysql::server::backup

See README.me for usage.


#### Parameters

The following parameters are available in the `mysql::server::backup` class.

##### `backupuser`

Data type: `Any`



Default value: `undef`

##### `backuppassword`

Data type: `Any`



Default value: `undef`

##### `backupdir`

Data type: `Any`



Default value: `undef`

##### `backupdirmode`

Data type: `Any`



Default value: '0700'

##### `backupdirowner`

Data type: `Any`



Default value: 'root'

##### `backupdirgroup`

Data type: `Any`



Default value: 'root'

##### `backupcompress`

Data type: `Any`



Default value: `true`

##### `backuprotate`

Data type: `Any`



Default value: 30

##### `ignore_events`

Data type: `Any`



Default value: `true`

##### `delete_before_dump`

Data type: `Any`



Default value: `false`

##### `backupdatabases`

Data type: `Any`



Default value: []

##### `file_per_database`

Data type: `Any`



Default value: `false`

##### `include_routines`

Data type: `Any`



Default value: `false`

##### `include_triggers`

Data type: `Any`



Default value: `false`

##### `ensure`

Data type: `Any`



Default value: 'present'

##### `time`

Data type: `Any`



Default value: ['23', '5']

##### `prescript`

Data type: `Any`



Default value: `false`

##### `postscript`

Data type: `Any`



Default value: `false`

##### `execpath`

Data type: `Any`



Default value: '/usr/bin:/usr/sbin:/bin:/sbin'

##### `provider`

Data type: `Any`



Default value: 'mysqldump'

##### `maxallowedpacket`

Data type: `Any`



Default value: '1M'

##### `optional_args`

Data type: `Any`



Default value: []


### mysql::server::binarylog

Binary log configuration requires the mysql user to be present. This must be done after package install


### mysql::server::config

See README.me for options.


### mysql::server::install

The mysql::server::install class.


### mysql::server::installdb

The mysql::server::installdb class.


### mysql::server::monitor

This is a helper class to add a monitoring user to the database


#### Parameters

The following parameters are available in the `mysql::server::monitor` class.

##### `mysql_monitor_username`

Data type: `Any`



Default value: ''

##### `mysql_monitor_password`

Data type: `Any`



Default value: ''

##### `mysql_monitor_hostname`

Data type: `Any`



Default value: ''


### mysql::server::mysqltuner

The mysql::server::mysqltuner class.


#### Parameters

The following parameters are available in the `mysql::server::mysqltuner` class.

##### `ensure`

Data type: `Any`



Default value: 'present'

##### `version`

Data type: `Any`



Default value: 'v1.3.0'

##### `source`

Data type: `Any`



Default value: `undef`

##### `environment`

Data type: `Any`



Default value: `undef`


### mysql::server::providers

Convenience class to call each of the three providers with the corresponding
hashes provided in mysql::server.
See README.md for details.


### mysql::server::root_password

The mysql::server::root_password class.


### mysql::server::service

The mysql::server::service class.


## Defined types

### mysql::db

See README.md for details.


#### Parameters

The following parameters are available in the `mysql::db` defined type.

##### `grant`

Data type: `Any`

do some shit

Default value: 'ALL'

##### `user`

Data type: `Any`



##### `password`

Data type: `Any`



##### `dbname`

Data type: `Any`



Default value: $name

##### `charset`

Data type: `Any`



Default value: 'utf8'

##### `collate`

Data type: `Any`



Default value: 'utf8_general_ci'

##### `host`

Data type: `Any`



Default value: 'localhost'

##### `sql`

Data type: `Optional[Variant[Array, Hash, String]]`



Default value: `undef`

##### `enforce_sql`

Data type: `Any`



Default value: `false`

##### `ensure`

Data type: `Enum['absent', 'present']`



Default value: 'present'

##### `import_timeout`

Data type: `Any`



Default value: 300

##### `import_cat_cmd`

Data type: `Any`



Default value: 'cat'


## Resource types

### mysql_database

Manage MySQL databases.


#### Properties

The following properties are available in the `mysql_database` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `charset`

Valid values: %r{^\S+$}

The CHARACTER SET setting for the database

Default value: utf8

##### `collate`

Valid values: %r{^\S+$}

The COLLATE setting for the database

Default value: utf8_general_ci

#### Parameters

The following parameters are available in the `mysql_database` type.

##### `name`

namevar

The name of the MySQL database to manage.


### mysql_datadir

Manage MySQL datadirs with mysql_install_db OR mysqld (5.7.6 and above).


#### Properties

The following properties are available in the `mysql_datadir` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

#### Parameters

The following parameters are available in the `mysql_datadir` type.

##### `datadir`

The datadir name

##### `basedir`

Valid values: %r{^/}

The basedir name, default /usr.

##### `user`

The user for the directory default mysql (name, not uid).

##### `defaults_extra_file`

Valid values: %r{^/.*\.cnf$}

MySQL defaults-extra-file with absolute path (*.cnf).

##### `insecure`

Insecure initialization (needed for 5.7.6++).

##### `log_error`

Valid values: %r{^/}

The path to the mysqld error log file (used with the --log-error option)


### mysql_grant

Manage a MySQL user's rights.


#### Properties

The following properties are available in the `mysql_grant` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `privileges`

Privileges for user

##### `table`

Valid values: %r{.*\..*}, %r{^[0-9a-zA-Z$_]*@[\w%\.:\-/]*$}

Table to apply privileges to.

##### `user`

User to operate on.

##### `options`

Options to grant.

#### Parameters

The following parameters are available in the `mysql_grant` type.

##### `name`

namevar

Name to describe the grant.


### mysql_plugin

Manage MySQL plugins.


#### Properties

The following properties are available in the `mysql_plugin` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `soname`

Valid values: %r{^\w+\.\w+$}

The name of the library

#### Parameters

The following parameters are available in the `mysql_plugin` type.

##### `name`

namevar

The name of the MySQL plugin to manage.


### mysql_user

Manage a MySQL user. This includes management of users password as well as privileges.


#### Properties

The following properties are available in the `mysql_user` type.

##### `ensure`

Valid values: present, absent

The basic property that the resource should be in.

Default value: present

##### `password_hash`

Valid values: %r{\w*}

The password hash of the user. Use mysql_password() for creating such a hash.

##### `plugin`

Valid values: %r{\w+}

The authentication plugin of the user.

##### `max_user_connections`

Valid values: %r{\d+}

Max concurrent connections for the user. 0 means no (or global) limit.

##### `max_connections_per_hour`

Valid values: %r{\d+}

Max connections per hour for the user. 0 means no (or global) limit.

##### `max_queries_per_hour`

Valid values: %r{\d+}

Max queries per hour for the user. 0 means no (or global) limit.

##### `max_updates_per_hour`

Valid values: %r{\d+}

Max updates per hour for the user. 0 means no (or global) limit.

##### `tls_options`

Options to that set the TLS-related REQUIRE attributes for the user.

#### Parameters

The following parameters are available in the `mysql_user` type.

##### `name`

namevar

The name of the user. This uses the 'username@hostname' or username@hostname.


## Functions

### mysql_deepmerge
Type: Ruby 3.x API

Recursively merges two or more hashes together and returns the resulting hash.

For example:

    $hash1 = {'one' => 1, 'two' => 2, 'three' => { 'four' => 4 } }
    $hash2 = {'two' => 'dos', 'three' => { 'five' => 5 } }
    $merged_hash = mysql_deepmerge($hash1, $hash2)
    # The resulting hash is equivalent to:
    # $merged_hash = { 'one' => 1, 'two' => 'dos', 'three' => { 'four' => 4, 'five' => 5 } }

When there is a duplicate key that is a hash, they are recursively merged.
When there is a duplicate key that is not a hash, the key in the rightmost hash will "win."
When there are conficting uses of dashes and underscores in two keys (which mysql would otherwise equate),
  the rightmost style will win.

#### `mysql_deepmerge()`

Recursively merges two or more hashes together and returns the resulting hash.

For example:

    $hash1 = {'one' => 1, 'two' => 2, 'three' => { 'four' => 4 } }
    $hash2 = {'two' => 'dos', 'three' => { 'five' => 5 } }
    $merged_hash = mysql_deepmerge($hash1, $hash2)
    # The resulting hash is equivalent to:
    # $merged_hash = { 'one' => 1, 'two' => 'dos', 'three' => { 'four' => 4, 'five' => 5 } }

When there is a duplicate key that is a hash, they are recursively merged.
When there is a duplicate key that is not a hash, the key in the rightmost hash will "win."
When there are conficting uses of dashes and underscores in two keys (which mysql would otherwise equate),
  the rightmost style will win.

Returns: `Any`

### mysql_dirname
Type: Ruby 3.x API

Returns the dirname of a path.

#### `mysql_dirname()`

Returns the dirname of a path.

Returns: `Any`

### mysql_password
Type: Ruby 3.x API

Returns the mysql password hash from the clear text password.

#### `mysql_password()`

Returns the mysql password hash from the clear text password.

Returns: `Any`

### mysql_strip_hash
Type: Ruby 3.x API

TEMPORARY FUNCTION: EXPIRES 2014-03-10
When given a hash this function strips out all blank entries.

#### `mysql_strip_hash()`

TEMPORARY FUNCTION: EXPIRES 2014-03-10
When given a hash this function strips out all blank entries.

Returns: `Any`

## Tasks

### export

Allows you to backup your database to local file.

#### Input

Input method: stdin

#### Parameters

##### `database`

Data type: `Optional[String[1]]`

Database to connect to

##### `user`

Data type: `Optional[String[1]]`

The user

##### `password`

Data type: `Optional[String[1]]`

The password

##### `file`

Data type: `String[1]`

Path to file you want backup to

### sql

Allows you to execute arbitary SQL

#### Input

Input method: stdin

#### Parameters

##### `database`

Data type: `Optional[String[1]]`

Database to connect to

##### `user`

Data type: `Optional[String[1]]`

The user

##### `password`

Data type: `Optional[String[1]]`

The password

##### `sql`

Data type: `String[1]`

The SQL you want to execute

