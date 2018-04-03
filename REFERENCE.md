# Reference

## Classes

### Public Classes

* [`mysql::backup::mysqlbackup`](#mysqlbackupmysqlbackup): 
* [`mysql::backup::mysqldump`](#mysqlbackupmysqldump): 
* [`mysql::backup::xtrabackup`](#mysqlbackupxtrabackup): 
* [`mysql::bindings`](#mysqlbindings): Parent class for MySQL bindings.
* [`mysql::bindings::daemon_dev`](#mysqlbindingsdaemon_dev): Private class
* [`mysql::bindings::java`](#mysqlbindingsjava): Private class
* [`mysql::bindings::perl`](#mysqlbindingsperl): Private class
* [`mysql::bindings::php`](#mysqlbindingsphp): Private class: See README.md
* [`mysql::bindings::python`](#mysqlbindingspython): Private class
* [`mysql::bindings::ruby`](#mysqlbindingsruby): Private class
* [`mysql::client`](#mysqlclient): Installs and configures the MySQL client.
* [`mysql::client::install`](#mysqlclientinstall): See README.md.
* [`mysql::params`](#mysqlparams): Private class: See README.md.
* [`mysql::server`](#mysqlserver): Installs and configures the MySQL server.
* [`mysql::server::account_security`](#mysqlserveraccount_security): See README.md.
* [`mysql::server::backup`](#mysqlserverbackup): 
* [`mysql::server::binarylog`](#mysqlserverbinarylog): Binary log configuration requires the mysql user to be present. This must be done after package install
* [`mysql::server::config`](#mysqlserverconfig): See README.me for options.
* [`mysql::server::monitor`](#mysqlservermonitor): Manage MySQL monitoring.
* [`mysql::server::mysqltuner`](#mysqlservermysqltuner): Manage the MySQLTuner package.
* [`mysql::server::providers`](#mysqlserverproviders): Convenience class to call each of the three providers with the corresponding hashes provided in mysql::server. See README.md for details.

### Private Classes

* `mysql::bindings::client_dev`: Private class
* `mysql::server::install`: Private class for managing MySQL package.
* `mysql::server::installdb`: 
* `mysql::server::root_password`: Private class for managing the root password
* `mysql::server::service`: Private class for managing the MySQL service

## Defined types

* [`mysql::db`](#mysqldb): Create and configure a MySQL database.

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

The mysql::backup::mysqlbackup class.

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

The mysql::backup::mysqldump class.

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

The mysql::backup::xtrabackup class.

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

Parent class for MySQL bindings.

#### Parameters

The following parameters are available in the `mysql::bindings` class.

##### `install_options`

Data type: `Any`

Passes `install_options` array to managed package resources. You must pass the [appropriate options](https://docs.puppetlabs.com/references/latest/type.html#package-attribute-install_options) for the package manager(s).

Default value: `undef`

##### `java_enable`

Data type: `Any`

Specifies whether `::mysql::bindings::java` should be included. Valid values are `true`, `false`.

Default value: `false`

##### `perl_enable`

Data type: `Any`

Specifies whether `mysql::bindings::perl` should be included. Valid values are `true`, `false`.

Default value: `false`

##### `php_enable`

Data type: `Any`

Specifies whether `mysql::bindings::php` should be included. Valid values are `true`, `false`.

Default value: `false`

##### `python_enable`

Data type: `Any`

Specifies whether `mysql::bindings::python` should be included. Valid values are `true`, `false`.

Default value: `false`

##### `ruby_enable`

Data type: `Any`

Specifies whether `mysql::bindings::ruby` should be included. Valid values are `true`, `false`.

Default value: `false`

##### `client_dev`

Data type: `Any`

Specifies whether `::mysql::bindings::client_dev` should be included. Valid values are `true`', `false`.

Default value: `false`

##### `daemon_dev`

Data type: `Any`

Specifies whether `::mysql::bindings::daemon_dev` should be included. Valid values are `true`, `false`.

Default value: `false`

##### `java_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `java_enable => true`.

Default value: $mysql::params::java_package_ensure

##### `java_package_name`

Data type: `Any`

The name of the Java package to install. Only applies if `java_enable => true`.

Default value: $mysql::params::java_package_name

##### `java_package_provider`

Data type: `Any`

The provider to use to install the Java package. Only applies if `java_enable => true`.

Default value: $mysql::params::java_package_provider

##### `perl_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `perl_enable => true`.

Default value: $mysql::params::perl_package_ensure

##### `perl_package_name`

Data type: `Any`

The name of the Perl package to install. Only applies if `perl_enable => true`.

Default value: $mysql::params::perl_package_name

##### `perl_package_provider`

Data type: `Any`

The provider to use to install the Perl package. Only applies if `perl_enable => true`.

Default value: $mysql::params::perl_package_provider

##### `php_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `php_enable => true`.

Default value: $mysql::params::php_package_ensure

##### `php_package_name`

Data type: `Any`

The name of the PHP package to install. Only applies if `php_enable => true`.

Default value: $mysql::params::php_package_name

##### `php_package_provider`

Data type: `Any`

The provider to use to install the PHP package. Only applies if `php_enable => true`.

Default value: $mysql::params::php_package_provider

##### `python_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `python_enable => true`.

Default value: $mysql::params::python_package_ensure

##### `python_package_name`

Data type: `Any`

The name of the Python package to install. Only applies if `python_enable => true`.

Default value: $mysql::params::python_package_name

##### `python_package_provider`

Data type: `Any`

The provider to use to install the Python package. Only applies if `python_enable => true`.

Default value: $mysql::params::python_package_provider

##### `ruby_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `ruby_enable => true`.

Default value: $mysql::params::ruby_package_ensure

##### `ruby_package_name`

Data type: `Any`

The name of the Ruby package to install. Only applies if `ruby_enable => true`.

Default value: $mysql::params::ruby_package_name

##### `ruby_package_provider`

Data type: `Any`

What provider should be used to install the package.

Default value: $mysql::params::ruby_package_provider

##### `client_dev_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `client_dev => true`.

Default value: $mysql::params::client_dev_package_ensure

##### `client_dev_package_name`

Data type: `Any`

The name of the client_dev package to install. Only applies if `client_dev => true`.

Default value: $mysql::params::client_dev_package_name

##### `client_dev_package_provider`

Data type: `Any`

The provider to use to install the client_dev package. Only applies if `client_dev => true`.

Default value: $mysql::params::client_dev_package_provider

##### `daemon_dev_package_ensure`

Data type: `Any`

Whether the package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Only applies if `daemon_dev => true`.

Default value: $mysql::params::daemon_dev_package_ensure

##### `daemon_dev_package_name`

Data type: `Any`

The name of the daemon_dev package to install. Only applies if `daemon_dev => true`.

Default value: $mysql::params::daemon_dev_package_name

##### `daemon_dev_package_provider`

Data type: `Any`

The provider to use to install the daemon_dev package. Only applies if `daemon_dev => true`.

Default value: $mysql::params::daemon_dev_package_provider

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

Installs and configures the MySQL client.

#### Parameters

The following parameters are available in the `mysql::client` class.

##### `bindings_enable`

Data type: `Any`

Whether to automatically install all bindings. Valid values are `true`, `false`. Default to `false`.

Default value: $mysql::params::bindings_enable

##### `install_options`

Data type: `Any`

Array of install options for managed package resources. You must pass the appropriate options for the package manager.

Default value: `undef`

##### `package_ensure`

Data type: `Any`

Whether the MySQL package should be present, absent, or a specific version. Valid values are 'present', 'absent', or 'x.y.z'.

Default value: $mysql::params::client_package_ensure

##### `package_manage`

Data type: `Any`

Whether to manage the MySQL client package. Defaults to `true`.

Default value: $mysql::params::client_package_manage

##### `package_name`

Data type: `Any`

The name of the MySQL client package to install.

Default value: $mysql::params::client_package_name

### mysql::client::install

See README.md.

### mysql::params

Private class: See README.md.

### mysql::server

Installs and configures the MySQL server.

#### Parameters

The following parameters are available in the `mysql::server` class.

##### `config_file`

Data type: `Any`

The location, as a path, of the MySQL configuration file.

Default value: $mysql::params::config_file

##### `includedir`

Data type: `Any`

The location, as a path, of !includedir for custom configuration overrides.

Default value: $mysql::params::includedir

##### `install_options`

Data type: `Any`

Passes [install_options](https://docs.puppetlabs.com/references/latest/type.html#package-attribute-install_options) array to managed package resources. You must pass the appropriate options for the specified package manager.

Default value: `undef`

##### `install_secret_file`

Data type: `Any`



Default value: $mysql::params::install_secret_file

##### `manage_config_file`

Data type: `Any`

Whether the MySQL configuration file should be managed. Valid values are `true`, `false`. Defaults to `true`.

Default value: $mysql::params::manage_config_file

##### `override_options`

Data type: `Any`

Specifies override options to pass into MySQL. Structured like a hash in the my.cnf file:  See  above for usage details.

Default value: {}

##### `package_ensure`

Data type: `Any`

Whether the package exists or should be a specific version. Valid values are 'present', 'absent', or 'x.y.z'. Defaults to 'present'.

Default value: $mysql::params::server_package_ensure

##### `package_manage`

Data type: `Any`

Whether to manage the MySQL server package. Defaults to `true`.

Default value: $mysql::params::server_package_manage

##### `package_name`

Data type: `Any`

The name of the MySQL server package to install.

Default value: $mysql::params::server_package_name

##### `purge_conf_dir`

Data type: `Any`

Whether the `includedir` directory should be purged. Valid values are `true`, `false`. Defaults to `false`.

Default value: $mysql::params::purge_conf_dir

##### `remove_default_accounts`

Data type: `Any`

Specifies whether to automatically include `mysql::server::account_security`. Valid values are `true`, `false`. Defaults to `false`.

Default value: `false`

##### `restart`

Data type: `Any`

Whether the service should be restarted when things change. Valid values are `true`, `false`. Defaults to `false`.

Default value: $mysql::params::restart

##### `root_group`

Data type: `Any`

The name of the group used for root. Can be a group name or a group ID. See more about the [group](https://docs.puppetlabs.com/references/latest/type.html#file-attribute-group).

Default value: $mysql::params::root_group

##### `mysql_group`

Data type: `Any`

The name of the group of the MySQL daemon user. Can be a group name or a group ID. See more about the [group](https://docs.puppetlabs.com/references/latest/type.html#file-attribute-group).

Default value: $mysql::params::mysql_group

##### `root_password`

Data type: `Any`

The MySQL root password. Puppet attempts to set the root password and update `/root/.my.cnf` with it. This is required if `create_root_user` or `create_root_my_cnf` are true. If `root_password` is 'UNSET', then `create_root_user` and `create_root_my_cnf` are assumed to be false --- that is, the MySQL root user and `/root/.my.cnf` are not created. Password changes are supported; however, the old password must be set in `/root/.my.cnf`. Effectively, Puppet uses the old password, configured in `/root/my.cnf`, to set the new password in MySQL, and then updates `/root/.my.cnf` with the new password.

Default value: $mysql::params::root_password

##### `service_enabled`

Data type: `Any`

Specifies whether the service should be enabled. Valid values are `true`, `false`. Defaults to `true`.

Default value: $mysql::params::server_service_enabled

##### `service_manage`

Data type: `Any`

Specifies whether the service should be managed. Valid values are `true`, `false`. Defaults to `true`.

Default value: $mysql::params::server_service_manage

##### `service_name`

Data type: `Any`

The name of the MySQL server service. Defaults are OS dependent, defined in 'params.pp'.

Default value: $mysql::params::server_service_name

##### `service_provider`

Data type: `Any`

The provider to use to manage the service. For Ubuntu, defaults to 'upstart'; otherwise, default is undefined.

Default value: $mysql::params::server_service_provider

##### `create_root_user`

Data type: `Any`

Whether root user should be created. Valid values are `true`, `false`. Defaults to `true`. This is useful for a cluster setup with Galera. The root user has to be created only once. You can set this parameter true on one node and set it to false on the remaining nodes.

Default value: $mysql::params::create_root_user

##### `create_root_my_cnf`

Data type: `Any`

Whether to create `/root/.my.cnf`. Valid values are `true`, `false`. Defaults to `true`. `create_root_my_cnf` allows creation of `/root/.my.cnf` independently of `create_root_user`. You can use this for a cluster setup with Galera where you want `/root/.my.cnf` to exist on all nodes.

Default value: $mysql::params::create_root_my_cnf

##### `users`

Data type: `Any`

Optional hash of users to create, which are passed to [mysql_user](#mysql_user).

Default value: {}

##### `grants`

Data type: `Any`

Optional hash of grants, which are passed to [mysql_grant](#mysql_grant).

Default value: {}

##### `databases`

Data type: `Any`

Optional hash of databases to create, which are passed to [mysql_database](#mysql_database).

Default value: {}

##### `enabled`

Data type: `Any`



Default value: `undef`

##### `manage_service`

Data type: `Any`



Default value: `undef`

##### `old_root_password`

Data type: `Any`

This parameter no longer does anything. It exists only for backwards compatibility. See the `root_password` parameter above for details on changing the root password.

Default value: `undef`

### mysql::server::account_security

See README.md.

### mysql::server::backup

The mysql::server::backup class.

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

A script that is executed before the backup begins.

Default value: `false`

##### `postscript`

Data type: `Any`

A script that is executed when the backup is finished. This could be used to sync the backup to a central store. This script can be either a single line that is directly executed or a number of lines supplied as an array. It could also be one or more externally managed (executable) files.

Default value: `false`

##### `execpath`

Data type: `Any`



Default value: '/usr/bin:/usr/sbin:/bin:/sbin'

##### `provider`

Data type: `Any`

Sets the server backup implementation. Valid values are:

Default value: 'mysqldump'

##### `maxallowedpacket`

Data type: `Any`

Defines the maximum SQL statement size for the backup dump script. The default value is 1MB, as this is the default MySQL Server value.

Default value: '1M'

##### `optional_args`

Data type: `Any`

Specifies an array of optional arguments which should be passed through to the backup tool. (Currently only supported by the xtrabackup provider.)

Default value: []

### mysql::server::binarylog

Binary log configuration requires the mysql user to be present. This must be done after package install

### mysql::server::config

See README.me for options.

### mysql::server::monitor

This is a helper class to add a monitoring user to the database

#### Parameters

The following parameters are available in the `mysql::server::monitor` class.

##### `mysql_monitor_username`

Data type: `Any`

The username to create for MySQL monitoring.

Default value: ''

##### `mysql_monitor_password`

Data type: `Any`

The password to create for MySQL monitoring.

Default value: ''

##### `mysql_monitor_hostname`

Data type: `Any`

The hostname from which the monitoring user requests are allowed access.

Default value: ''

### mysql::server::mysqltuner

Manage the MySQLTuner package.

#### Parameters

The following parameters are available in the `mysql::server::mysqltuner` class.

##### `ensure`

Data type: `Any`

Ensures that the resource exists. Valid values are 'present', 'absent'. Defaults to 'present'.

Default value: 'present'

##### `version`

Data type: `Any`

The version to install from the major/MySQLTuner-perl github repository. Must be a valid tag. Defaults to 'v1.3.0'.

Default value: 'v1.3.0'

##### `source`

Data type: `Any`



Default value: `undef`

##### `environment`

Data type: `Any`

Environment variables active during download, e.g. to download via proxies: environment => 'https_proxy=http://proxy.example.com:80'

Default value: `undef`

### mysql::server::providers

Convenience class to call each of the three providers with the corresponding
hashes provided in mysql::server.
See README.md for details.

## Defined types

### mysql::db

Create and configure a MySQL database.

#### Parameters

The following parameters are available in the `mysql::db` defined type.

##### `user`

Data type: `Any`

The user for the database you're creating.

##### `password`

Data type: `Any`

The password for $user for the database you're creating.

##### `dbname`

Data type: `Any`

The name of the database to create.

Default value: $name

##### `charset`

Data type: `Any`

The character set for the database.

Default value: 'utf8'

##### `collate`

Data type: `Any`

The collation for the database.

Default value: 'utf8_general_ci'

##### `host`

Data type: `Any`

The host to use as part of user@host for grants.

Default value: 'localhost'

##### `grant`

Data type: `Any`

The privileges to be granted for user@host on the database.

Default value: 'ALL'

##### `sql`

Data type: `Optional[Variant[Array, Hash, String]]`

The path to the sqlfile you want to execute. This can be single file specified as string, or it can be an array of strings.

Default value: `undef`

##### `enforce_sql`

Data type: `Any`

Specifies whether executing the sqlfiles should happen on every run. If set to false, sqlfiles only run once.

Default value: `false`

##### `ensure`

Data type: `Enum['absent', 'present']`

Specifies whether to create the database. Valid values are 'present', 'absent'. Defaults to 'present'.

Default value: 'present'

##### `import_timeout`

Data type: `Any`

Timeout, in seconds, for loading the sqlfiles. Defaults to 300.

Default value: 300

##### `import_cat_cmd`

Data type: `Any`

Command to read the sqlfile for importing the database. Useful for compressed sqlfiles. For example, you can use 'zcat' for .gz files.

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

**Supports noop?** false

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

**Supports noop?** false

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

