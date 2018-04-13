# mysql

#### Table of Contents

1. [Module Description - What the module does and why it is useful](#module-description)
2. [Setup - The basics of getting started with mysql](#setup)
    * [Beginning with mysql](#beginning-with-mysql)
3. [Usage - Configuration options and additional functionality](#usage)
    * [Customize server options](#customize-server-options)
    * [Create a database](#create-a-database)
    * [Customize configuration](#customize-configuration)
    * [Work with an existing server](#work-with-an-existing-server)
    * [Specify passwords](#specify-passwords)
    * [Install Percona server on CentOS](#install-percona-server-on-centos)
    * [Install MariaDB on Ubuntu](#install-mariadb-on-ubuntu)
4. [Reference - An under-the-hood peek at what the module is doing and how](#reference)
5. [Limitations - OS compatibility, etc.](#limitations)
6. [Development - Guide for contributing to the module](#development)

## Module Description

The mysql module installs, configures, and manages the MySQL service.

This module manages both the installation and configuration of MySQL, as well as extending Puppet to allow management of MySQL resources, such as databases, users, and grants.

## Setup

### Beginning with mysql

To install a server with the default options:

`include '::mysql::server'`.

To customize options, such as the root password or `/etc/my.cnf` settings, you must also pass in an override hash:

```puppet
class { '::mysql::server':
  root_password           => 'strongpassword',
  remove_default_accounts => true,
  override_options        => $override_options
}
```

See [**Customize Server Options**](#customize-server-options) below for examples of the hash structure for $override_options.

## Usage

All interaction for the server is done via `mysql::server`. To install the client, use `mysql::client`. To install bindings, use `mysql::bindings`.

### Customize server options

To define server options, structure a hash structure of overrides in `mysql::server`. This hash resembles a hash in the my.cnf file:

```puppet
$override_options = {
  'section' => {
    'item' => 'thing',
  }
}
```

For options that you would traditionally represent in this format:

```
[section]
thing = X
```

Entries can be created as `thing => true`, `thing => value`, or `thing => ""` in the hash. Alternatively, you can pass an array as `thing => ['value', 'value2']` or list each `thing => value` separately on individual lines.

You can pass a variable in the hash without setting a value for it; the variable would then use MySQL's default settings. To exclude an option from the `my.cnf` file --- for example, when using `override_options` to revert to a default value --- pass `thing => undef`.

If an option needs multiple instances, pass an array. For example,

```puppet
$override_options = {
  'mysqld' => {
    'replicate-do-db' => ['base1', 'base2'],
  }
}
```

produces

```puppet
[mysqld]
replicate-do-db = base1
replicate-do-db = base2
```

To implement version specific parameters, specify the version, such as [mysqld-5.5]. This allows one config for different versions of MySQL.

### Create a database

To create a database with a user and some assigned privileges:

```puppet
mysql::db { 'mydb':
  user     => 'myuser',
  password => 'mypass',
  host     => 'localhost',
  grant    => ['SELECT', 'UPDATE'],
}
```

To use a different resource name with exported resources:

```puppet
 @@mysql::db { "mydb_${fqdn}":
  user     => 'myuser',
  password => 'mypass',
  dbname   => 'mydb',
  host     => ${fqdn},
  grant    => ['SELECT', 'UPDATE'],
  tag      => $domain,
}
```

Then you can collect it on the remote DB server:

```puppet
Mysql::Db <<| tag == $domain |>>
```

If you set the sql parameter to a file when creating a database, the file is imported into the new database.

For large sql files, increase the `import_timeout` parameter, which defaults to 300 seconds.

```puppet
mysql::db { 'mydb':
  user     => 'myuser',
  password => 'mypass',
  host     => 'localhost',
  grant    => ['SELECT', 'UPDATE'],
  sql      => '/path/to/sqlfile.gz',
  import_cat_cmd => 'zcat',
  import_timeout => 900,
}
```

### Customize configuration

To add custom MySQL configuration, place additional files into `includedir`. This allows you to override settings or add additional ones, which is helpful if you don't use `override_options` in `mysql::server`. The `includedir` location is by default set to `/etc/mysql/conf.d`.

### Work with an existing server

To instantiate databases and users on an existing MySQL server, you need a `.my.cnf` file in `root`'s home directory. This file must specify the remote server address and credentials. For example:

```puppet
[client]
user=root
host=localhost
password=secret
```

This module uses the `mysqld_version` fact to discover the server version being used.  By default, this is set to the output of `mysqld -V`.  If you're working with a remote MySQL server, you may need to set a custom fact for `mysqld_version` to ensure correct behaviour.

When working with a remote server, do *not* use the `mysql::server` class in your Puppet manifests.

### Specify passwords

In addition to passing passwords as plain text, you can input them as hashes. For example:

```puppet
mysql::db { 'mydb':
  user     => 'myuser',
  password => '*6C8989366EAF75BB670AD8EA7A7FC1176A95CEF4',
  host     => 'localhost',
  grant    => ['SELECT', 'UPDATE'],
}
```

### Install Percona server on CentOS

This example shows how to do a minimal installation of a Percona server on a
CentOS system. This sets up the Percona server, client, and bindings (including Perl and Python bindings). You can customize this usage and update the version as needed.

This usage has been tested on Puppet 4.4 / CentOS 7 / Percona Server 5.7.

**Note:** The installation of the yum repository is not part of this package
and is here only to show a full example of how you can install.

```puppet
yumrepo { 'percona':
  descr    => 'CentOS $releasever - Percona',
  baseurl  => 'http://repo.percona.com/centos/$releasever/os/$basearch/',
  gpgkey   => 'http://www.percona.com/downloads/percona-release/RPM-GPG-KEY-percona',
  enabled  => 1,
  gpgcheck => 1,
}

class {'mysql::server':
  package_name     => 'Percona-Server-server-57',
  package_ensure   => '5.7.11-4.1.el7',
  service_name     => 'mysql',
  config_file      => '/etc/my.cnf',
  includedir       => '/etc/my.cnf.d',
  root_password    => 'PutYourOwnPwdHere',
  override_options => {
    mysqld => {
      log-error => '/var/log/mysqld.log',
      pid-file  => '/var/run/mysqld/mysqld.pid',
    },
    mysqld_safe => {
      log-error => '/var/log/mysqld.log',
    },
  }
}

# Note: Installing Percona-Server-server-57 also installs Percona-Server-client-57.
# This shows how to install the Percona MySQL client on its own
class {'mysql::client':
  package_name   => 'Percona-Server-client-57',
  package_ensure => '5.7.11-4.1.el7',
}

# These packages are normally installed along with Percona-Server-server-57
# If you needed to install the bindings, however, you could do so with this code
class { 'mysql::bindings':
  client_dev_package_name   => 'Percona-Server-shared-57',
  client_dev_package_ensure => '5.7.11-4.1.el7',
  client_dev                => true,
  daemon_dev_package_name   => 'Percona-Server-devel-57',
  daemon_dev_package_ensure => '5.7.11-4.1.el7',
  daemon_dev                => true,
  perl_enable               => true,
  perl_package_name         => 'perl-DBD-MySQL',
  python_enable             => true,
  python_package_name       => 'MySQL-python',
}

# Dependencies definition
Yumrepo['percona']->
Class['mysql::server']

Yumrepo['percona']->
Class['mysql::client']

Yumrepo['percona']->
Class['mysql::bindings']
```

### Install MariaDB on Ubuntu

#### Optional: Install the MariaDB official repo

In this example, we'll use the latest stable (currently 10.1) from the official MariaDB repository, not the one from the distro repository. You could instead use the package from the Ubuntu repository. Make sure you use the repository corresponding to the version you want.

**Note:** `sfo1.mirrors.digitalocean.com` is one of many mirrors available. You can use any official mirror.

```puppet
include apt

apt::source { 'mariadb':
  location => 'http://sfo1.mirrors.digitalocean.com/mariadb/repo/10.1/ubuntu',
  release  => $::lsbdistcodename,
  repos    => 'main',
  key      => {
    id     => '199369E5404BD5FC7D2FE43BCBCB082A1BB943DB',
    server => 'hkp://keyserver.ubuntu.com:80',
  },
  include => {
    src   => false,
    deb   => true,
  },
}
```

#### Install the MariaDB server

This example shows MariaDB server installation on Ubuntu Trusty. Adjust the version and the parameters of `my.cnf` as needed. All parameters of the `my.cnf` can be defined using the `override_options` parameter.

The folders `/var/log/mysql` and `/var/run/mysqld` are created automatically, but if you are using other custom folders, they should exist as prerequisites for this code.

All the values set here are an example of a working minimal configuration.

Specify the version of the package you want with the `package_ensure` parameter.

```puppet
class {'::mysql::server':
  package_name     => 'mariadb-server',
  package_ensure   => '10.1.14+maria-1~trusty',
  service_name     => 'mysql',
  root_password    => 'AVeryStrongPasswordUShouldEncrypt!',
  override_options => {
    mysqld => {
      'log-error' => '/var/log/mysql/mariadb.log',
      'pid-file'  => '/var/run/mysqld/mysqld.pid',
    },
    mysqld_safe => {
      'log-error' => '/var/log/mysql/mariadb.log',
    },
  }
}

# Dependency management. Only use that part if you are installing the repository
# as shown in the Preliminary step of this example.
Apt::Source['mariadb'] ~>
Class['apt::update'] ->
Class['::mysql::server']

```

#### Install the MariaDB client

This example shows how to install the MariaDB client and all of the bindings at once. You can do this installation separately from the server installation.

Specify the version of the package you want with the `package_ensure` parameter.

```puppet
class {'::mysql::client':
  package_name    => 'mariadb-client',
  package_ensure  => '10.1.14+maria-1~trusty',
  bindings_enable => true,
}

# Dependency management. Only use that part if you are installing the repository as shown in the Preliminary step of this example.
Apt::Source['mariadb'] ~>
Class['apt::update'] ->
Class['::mysql::client']
```

### Install MySQL Community server on CentOS

You can install MySQL Community Server on CentOS using the mysql module and Hiera. This example was tested with the following versions:

* MySQL Community Server 5.6
* Centos 7.3
* Puppet 3.8.7 using Hiera
* puppetlabs-mysql module v3.9.0

In Puppet:

```puppet
include ::mysql::server

create_resources(yumrepo, hiera('yumrepo', {}))

Yumrepo['repo.mysql.com'] -> Anchor['mysql::server::start']
Yumrepo['repo.mysql.com'] -> Package['mysql_client']

create_resources(mysql::db, hiera('mysql::server::db', {}))
```

In Hiera:

```yaml
---

# Centos 7.3
yumrepo:
  'repo.mysql.com':
    baseurl: "http://repo.mysql.com/yum/mysql-5.6-community/el/%{::operatingsystemmajrelease}/$basearch/"
    descr: 'repo.mysql.com'
    enabled: 1
    gpgcheck: true
    gpgkey: 'http://repo.mysql.com/RPM-GPG-KEY-mysql'

mysql::client::package_name: "mysql-community-client" # required for proper MySQL installation
mysql::server::package_name: "mysql-community-server" # required for proper MySQL installation
mysql::server::package_ensure: 'installed' # do not specify version here, unfortunately yum fails with error that package is already installed
mysql::server::root_password: "change_me_i_am_insecure"
mysql::server::manage_config_file: true
mysql::server::service_name: 'mysqld' # required for puppet module
mysql::server::override_options:
  'mysqld':
    'bind-address': '127.0.0.1'
    'log-error': '/var/log/mysqld.log' # required for proper MySQL installation
  'mysqld_safe':
    'log-error': '/var/log/mysqld.log'  # required for proper MySQL installation

# create database + account with access, passwords are not encrypted
mysql::server::db:
  "dev":
    user: "dev"
    password: "devpass"
    host: "127.0.0.1"
    grant:
      - "ALL"

```

### Tasks

The MySQL module has an example task that allows a user to execute arbitary SQL against a database. Please refer to to the [PE documentation](https://puppet.com/docs/pe/2017.3/orchestrator/running_tasks.html) or [Bolt documentation](https://puppet.com/docs/bolt/latest/bolt.html) on how to execute a task.

# Reference

## Classes

### Public Classes

* [`mysql::bindings`](#mysqlbindings): Parent class for MySQL bindings.
* [`mysql::client`](#mysqlclient): Installs and configures the MySQL client.
* [`mysql::server`](#mysqlserver): Installs and configures the MySQL server.
* [`mysql::server::backup`](#mysqlserverbackup): Create and manage a MySQL backup.
* [`mysql::server::monitor`](#mysqlservermonitor): This is a helper class to add a monitoring user to the database
* [`mysql::server::mysqltuner`](#mysqlservermysqltuner): Manage the MySQLTuner package.

### Private Classes

* `mysql::backup::mysqlbackup`: Manage the mysqlbackup client.
* `mysql::backup::mysqldump`: "Provider" for mysqldump
* `mysql::backup::xtrabackup`: "Provider" for Percona XtraBackup
* `mysql::bindings::client_dev`: Private class for installing client development bindings
* `mysql::bindings::daemon_dev`: Private class for installing daemon development bindings
* `mysql::bindings::java`: Private class for installing java language bindings.
* `mysql::bindings::perl`: Private class for installing perl language bindings.
* `mysql::bindings::php`: Private class for installing php language bindings
* `mysql::bindings::python`: Private class for installing python language bindings
* `mysql::bindings::ruby`: Private class for installing ruby language bindings
* `mysql::client::install`: Private class for MySQL client install.
* `mysql::params`: Params class.
* `mysql::server::account_security`: Private class for ensuring localhost accounts do not exist
* `mysql::server::binarylog`: Binary log configuration requires the mysql user to be present. This must be done after package install
* `mysql::server::config`: Private class for MySQL server configuration.
* `mysql::server::install`: Private class for managing MySQL package.
* `mysql::server::installdb`: Builds initial databases on installation.
* `mysql::server::providers`: Convenience class to call each of the three providers with the corresponding
hashes provided in mysql::server.
* `mysql::server::root_password`: Private class for managing the root password
* `mysql::server::service`: Private class for managing the MySQL service

## Defined types

* [`mysql::db`](#mysqldb): Create and configure a MySQL database.

## Resource types

### Public Resource types

* [`mysql_plugin`](#mysql_plugin): Manage MySQL plugins.

### Private Resource types

* `mysql_database`: Manage a MySQL database.
* `mysql_datadir`: Manage MySQL datadirs with mysql_install_db OR mysqld (5.7.6 and above).
* `mysql_grant`: Manage a MySQL user's rights.
* `mysql_user`: Manage a MySQL user. This includes management of users password as well as privileges.

## Functions

* [`mysql_deepmerge`](#mysql_deepmerge): Recursively merges two or more hashes together and returns the resulting hash.
* [`mysql_dirname`](#mysql_dirname): Returns the dirname of a path
* [`mysql_password`](#mysql_password): Hash a string as mysql's "PASSWORD()" function would do it
* [`mysql_strip_hash`](#mysql_strip_hash): TEMPORARY FUNCTION: EXPIRES 2014-03-10 When given a hash this function strips out all blank entries.

## Tasks

* [`export`](#export): Allows you to backup your database to local file.
* [`sql`](#sql): Allows you to execute arbitary SQL

## Classes

### mysql::bindings

Parent class for MySQL bindings.

#### Examples

##### Install Ruby language bindings

```puppet
class { 'mysql::bindings':
  ruby_enable           => true,
  ruby_package_ensure   => 'present',
  ruby_package_name     => 'ruby-mysql-2.7.1-1mdv2007.0.sparc.rpm',
  ruby_package_provider => 'rpm',
}
```

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

### mysql::client

Installs and configures the MySQL client.

#### Examples

##### Install the MySQL client

```puppet
class {'::mysql::client':
  package_name    => 'mysql-client',
  package_ensure  => 'present',
  bindings_enable => true,
}
```

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

### mysql::server

Installs and configures the MySQL server.

#### Examples

##### Install MySQL Server

```puppet
class { '::mysql::server':
  package_name            => 'mysql-server',
  package_ensure          => '5.7.1+mysql~trusty',
  root_password           => 'strongpassword',
  remove_default_accounts => true,
}
```

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

Passes [install_options](https://docs.puppetlabs.com/references/latest/type.html#package-attribute-install_options) array to managed package resources. You must pass the appropriate options for the specified package manager

Default value: `undef`

##### `install_secret_file`

Data type: `Any`

Path to secret file containing temporary root password.

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

_Deprecated_

Default value: `undef`

##### `manage_service`

Data type: `Any`

_Deprecated_

Default value: `undef`

##### `old_root_password`

Data type: `Any`

This parameter no longer does anything. It exists only for backwards compatibility. See the `root_password` parameter above for details on changing the root password.

Default value: `undef`

### mysql::server::backup

Create and manage a MySQL backup.

#### Examples

##### Create a basic MySQL backup:

```puppet
class { 'mysql::server':
  root_password => 'password'
}
class { 'mysql::server::backup':
  backupuser     => 'myuser',
  backuppassword => 'mypassword',
  backupdir      => '/tmp/backups',
}
```

#### Parameters

The following parameters are available in the `mysql::server::backup` class.

##### `backupuser`

Data type: `Any`

MySQL user with backup administrator privileges.

Default value: `undef`

##### `backuppassword`

Data type: `Any`

Password for `backupuser`.

Default value: `undef`

##### `backupdir`

Data type: `Any`

Directory to store backup.

Default value: `undef`

##### `backupdirmode`

Data type: `Any`

Permissions applied to the backup directory. This parameter is passed directly to the file resource.

Default value: '0700'

##### `backupdirowner`

Data type: `Any`

Owner for the backup directory. This parameter is passed directly to the file resource.

Default value: 'root'

##### `backupdirgroup`

Data type: `Any`

Group owner for the backup directory. This parameter is passed directly to the file resource.

Default value: 'root'

##### `backupcompress`

Data type: `Any`

Whether or not to compress the backup (when using the mysqldump provider)

Default value: `true`

##### `backuprotate`

Data type: `Any`

Backup rotation interval in 24 hour periods.

Default value: 30

##### `ignore_events`

Data type: `Any`

Ignore the mysql.event table.

Default value: `true`

##### `delete_before_dump`

Data type: `Any`

Whether to delete old .sql files before backing up. Setting to true deletes old files before backing up, while setting to false deletes them after backup.

Default value: `false`

##### `backupdatabases`

Data type: `Any`

Databases to backup (if using xtrabackup provider).

Default value: []

##### `file_per_database`

Data type: `Any`

Use file per database mode creating one file per database backup.

Default value: `false`

##### `include_routines`

Data type: `Any`

Dump stored routines (procedures and functions) from dumped databases when doing a `file_per_database` backup.

Default value: `false`

##### `include_triggers`

Data type: `Any`

Dump triggers for each dumped table when doing a `file_per_database` backup.

Default value: `false`

##### `ensure`

Data type: `Any`



Default value: 'present'

##### `time`

Data type: `Any`

An array of two elements to set the backup time. Allows ['23', '5'] (i.e., 23:05) or ['3', '45'] (i.e., 03:45) for HH:MM times.

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

Allows you to set a custom PATH should your MySQL installation be non-standard places. Defaults to `/usr/bin:/usr/sbin:/bin:/sbin`.

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

Source path for the mysqltuner package.

Default value: `undef`

##### `environment`

Data type: `Any`

Environment variables active during download, e.g. to download via proxies: environment => 'https_proxy=http://proxy.example.com:80'

Default value: `undef`

## Defined types

### mysql::db

Create and configure a MySQL database.

#### Examples

##### Create a database

```puppet
mysql::db { 'mydb':
  user     => 'myuser',
  password => 'mypass',
  host     => 'localhost',
  grant    => ['SELECT', 'UPDATE'],
}
```

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

### mysql_plugin

Manage MySQL plugins.

#### Examples

##### 

```puppet
mysql_plugin { 'some_plugin':
  soname => 'some_pluginlib.so',
}
```

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

## Functions

### mysql_deepmerge

Type: Ruby 3.x API

- When there is a duplicate key that is a hash, they are recursively merged.
- When there is a duplicate key that is not a hash, the key in the rightmost hash will "win."
- When there are conficting uses of dashes and underscores in two keys (which mysql would otherwise equate),
  the rightmost style will win.

#### `mysql_deepmerge()`

- When there is a duplicate key that is a hash, they are recursively merged.
- When there is a duplicate key that is not a hash, the key in the rightmost hash will "win."
- When there are conficting uses of dashes and underscores in two keys (which mysql would otherwise equate),
  the rightmost style will win.

Returns: `Hash`

### mysql_dirname

Type: Ruby 3.x API

Returns the dirname of a path

#### `mysql_dirname(String $path)`

Returns: `String` Directory name of path.

##### `path`

Data type: `String`

Path to find the dirname for.

### mysql_password

Type: Ruby 3.x API

Hash a string as mysql's "PASSWORD()" function would do it

#### `mysql_password(String $password)`

Returns: `String` the mysql password hash from the clear text password.

##### `password`

Data type: `String`

Plain text password.

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


## Limitations

This module has been tested on:

* RedHat Enterprise Linux 5, 6, 7
* Debian 6, 7, 8
* CentOS 5, 6, 7
* Ubuntu 10.04, 12.04, 14.04, 16.04
* Scientific Linux 5, 6
* SLES 11

Testing on other platforms has been minimal and cannot be guaranteed.

**Note:** The mysqlbackup.sh does not work and is not supported on MySQL 5.7 and greater.

Debian 9 compatibility has not been fully verified.

## Development

Puppet modules on the Puppet Forge are open projects, and community contributions are essential for keeping them great. We can't access the huge number of platforms and myriad of hardware, software, and deployment configurations that Puppet is intended to serve.

We want to keep it as easy as possible to contribute changes so that our modules work in your environment. There are a few guidelines that we need contributors to follow so that we can have a chance of keeping on top of things.

Check out our the complete [module contribution guide](https://docs.puppetlabs.com/forge/contributing.html).

### Authors

This module is based on work by David Schmitt. The following contributors have contributed to this module (beyond Puppet Labs):

* Larry Ludwig
* Christian G. Warden
* Daniel Black
* Justin Ellison
* Lowe Schmidt
* Matthias Pigulla
* William Van Hevelingen
* Michael Arnold
* Chris Weyl
* Daniël van Eeden
* Jan-Otto Kröpke
* Timothy Sven Nelson
