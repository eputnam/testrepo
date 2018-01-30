# Reference
## Classes
* [`ntp`](#ntp): ntp

Main class, includes all other classes.
* [`ntp::config`](#ntpconfig): This class handles the configuration file. Avoid modifying private classes.
* [`ntp::install`](#ntpinstall): This class handles ntp packages. Avoid modifying private classes.
* [`ntp::service`](#ntpservice): This class handles the ntp service. Avoid modifying private classes.
## Defined types
* [`ntp::qux`](#ntpqux): this is the qux type
## Resource types
* [`test`](#test): eowjoijewfiojewf
## Functions
* [`dope`](#dope): This is a summary
* [`example`](#example): An example function written in Pupppet.
## Classes

### ntp

* **Since** 1.0.0

* **See also**
this
thing


#### Parameters

The following parameters are available in the ntp class.

##### `authprov`

Data type: Optional[String]

Enables compatibility with W32Time in some versions of NTPd (such as Novell DSfW). Default value: undef.
@since 1.1.0

##### `broadcastclient`

Data type: Boolean

Enables reception of broadcast server messages to any local interface. Default value: false.

##### `config`

Data type: Stdlib::Absolutepath

Specifies a file for NTP's configuration info. Default value: '/etc/ntp.conf' (or '/etc/inet/ntp.conf' on Solaris).

##### `config_dir`

Data type: Optional[Stdlib::Absolutepath]

Specifies a directory for the NTP configuration files. Default value: undef.

##### `config_epp`

Data type: Optional[String]

Specifies an absolute or relative file path to an EPP template for the config file.
Example value: 'ntp/ntp.conf.epp'. A validation error is thrown if both this **and** the `config_template` parameter are specified.

##### `config_file_mode`

Data type: String

Specifies a file mode for the ntp configuration file. Default value: '0664'.

##### `config_template`

Data type: Optional[String]

Specifies an absolute or relative file path to an ERB template for the config file.
Example value: 'ntp/ntp.conf.erb'. A validation error is thrown if both this **and** the `config_epp` parameter are specified.

##### `disable_auth`

Data type: Boolean

Disables cryptographic authentication for broadcast client, multicast client, and symmetric passive associations.

##### `disable_dhclient`

Data type: Boolean

Disables `ntp-servers` in `dhclient.conf` to prevent Dhclient from managing the NTP configuration.

##### `disable_kernel`

Data type: Boolean

Disables kernel time discipline.

##### `disable_monitor`

Data type: Boolean

Disables the monitoring facility in NTP. Default value: true.

##### `driftfile`

Data type: Stdlib::Absolutepath

Specifies an NTP driftfile. Default value: '/var/lib/ntp/drift' (except on AIX and Solaris).

##### `enable_mode7`

Data type: Boolean

Enables processing of NTP mode 7 implementation-specific requests which are used by the deprecated ntpdc program. Default value: false.

##### `fudge`

Data type: Optional[Array[String]]

Provides additional information for individual clock drivers. Default value: [ ]

##### `iburst_enable`

Data type: Boolean

Specifies whether to enable the iburst option for every NTP peer. Default value: false (true on AIX and Debian).

##### `interfaces`

Data type: Array[String]

Specifies one or more network interfaces for NTP to listen on. Default value: [ ].

##### `interfaces_ignore`

Data type: Array[String]

Specifies one or more ignore pattern for the NTP listener configuration (for example: all, wildcard, ipv6). Default value: [ ].

##### `keys`

Data type: Array[String]

Distributes keys to keys file. Default value: [ ].

##### `keys_controlkey`

Data type: Optional[Ntp::Key_id]

Specifies the key identifier to use with the ntpq utility. Value in the range of 1 to 65,534 inclusive. Default value: ' '.

##### `keys_enable`

Data type: Boolean

Whether to enable key-based authentication. Default value: false.

##### `keys_file`

Data type: Stdlib::Absolutepath

Specifies the complete path and location of the MD5 key file containing the keys and key identifiers used by ntpd, ntpq and ntpdc
when operating with symmetric key cryptography. Default value: `/etc/ntp.keys` (on RedHat and Amazon, `/etc/ntp/keys`).

##### `keys_requestkey`

Data type: Optional[Ntp::Key_id]

Specifies the key identifier to use with the ntpdc utility program. Value in the range of 1 to 65,534. Default value: ' '.

##### `keys_trusted`

Data type: Optional[Array[Ntp::Key_id]]

Provides one or more keys to be trusted by NTP. Default value: [ ].

##### `leapfile`

Data type: Optional[Stdlib::Absolutepath]

Specifies a leap second file for NTP to use. Default value: ' '.

##### `logfile`

Data type: Optional[Stdlib::Absolutepath]

Specifies a log file for NTP to use instead of syslog. Default value: ' '.

##### `minpoll`

Data type: Optional[Ntp::Poll_interval]

Sets Puppet to non-standard minimal poll interval of upstream servers.
Values: 3 to 16. Default: undef.

##### `maxpoll`

Data type: Optional[Ntp::Poll_interval]

Sets use non-standard maximal poll interval of upstream servers.
Values: 3 to 16. Default option: undef, except on FreeBSD (on FreeBSD, defaults to 9).

##### `ntpsigndsocket`

Data type: Optional[Stdlib::Absolutepath]

Sets NTP to sign packets using the socket in the ntpsigndsocket path. Requires NTP to be configured to sign sockets.
Value: Path to the socket directory; for example, for Samba: `usr/local/samba/var/lib/ntp_signd/`. Default value: undef.

##### `package_ensure`

Data type: String

Whether to install the NTP package, and what version to install. Values: 'present', 'latest', or a specific version number.
Default value: 'present'.

##### `package_manage`

Data type: Boolean

Whether to manage the NTP package. Default value: true.

##### `package_name`

Data type: Array[String]

Specifies the NTP package to manage. Default value: ['ntp'] (except on AIX and Solaris).

##### `panic`

Data type: Optional[Integer[0]]

Whether NTP should "panic" in the event of a very large clock skew. Applies only if `tinker` option set to true or if your environment
is in a virtual machine. Default value: 0 if environment is virtual, undef in all other cases.

##### `peers`

Data type: Array[String]

List of NTP servers with which to synchronise the local clock.

##### `pool`

Data type: Optional[Array[String]]

List of NTP server pools with which to synchronise the local clock.

##### `preferred_servers`

Data type: Array[String]

Specifies one or more preferred peers. Puppet appends 'prefer' to each matching item in the `servers` array.
Default value: [ ].

##### `noselect_servers`

Data type: Array[String]

Specifies one or more peers to not sync with. Puppet appends 'noselect' to each matching item in the `servers` array.
Default value: [ ].

##### `restrict`

Data type: Array[String]

Specifies one or more `restrict` options for the NTP configuration.
Puppet prefixes each item with 'restrict', so you need to list only the content of the restriction.
Default value for most operating systems:
  '[default kod nomodify notrap nopeer noquery', '-6 default kod nomodify notrap nopeer noquery', '127.0.0.1', '-6 ::1']'.
Default value for AIX systems:
  '['default nomodify notrap nopeer noquery', '127.0.0.1',]'.

##### `servers`

Data type: Array[String]

Specifies one or more servers to be used as NTP peers. Default value: varies by operating system.

##### `service_enable`

Data type: Boolean

Whether to enable the NTP service at boot. Default value: true.

##### `service_ensure`

Data type: Enum['running', 'stopped']

Whether the NTP service should be running. Default value: 'running'.

##### `service_manage`

Data type: Boolean

Whether to manage the NTP service.  Default value: true.

##### `service_name`

Data type: String

The NTP service to manage. Default value: varies by operating system.

##### `service_provider`

Data type: Optional[String]

Which service provider to use for NTP. Default value: 'undef'.

##### `statistics`

Data type: Optional[Array]

List of statistics to have NTP generate and keep. Default value: [ ].

##### `statsdir`

Data type: Optional[Stdlib::Absolutepath]

Location of the NTP statistics directory on the managed system. Default value: '/var/log/ntpstats'.

##### `step_tickers_file`

Data type: Optional[Stdlib::Absolutepath]

Location of the step tickers file on the managed system. Default value: varies by operating system.

##### `step_tickers_epp`

Data type: Optional[String]

Location of the step tickers EPP template file. Default value: varies by operating system.
Validation error is thrown if both this and the `step_tickers_template` parameters are specified.

##### `step_tickers_template`

Data type: Optional[String]

Location of the step tickers ERB template file. Default value: varies by operating system.
Validation error is thrown if both this and the `step_tickers_epp` parameter are specified.

##### `stepout`

Data type: Optional[Integer[0, 65535]]

Value for stepout if `tinker` value is true. Valid options: unsigned shortint digit. Default value: undef.

##### `tos`

Data type: Boolean

Whether to enable tos options. Default value: false.

##### `tos_minclock`

Data type: Optional[Integer[1]]

Specifies the minclock tos option. Default value: 3.

##### `tos_minsane`

Data type: Optional[Integer[1]]

Specifies the minsane tos option. Default value: 1.

##### `tos_floor`

Data type: Optional[Integer[1]]

Specifies the floor tos option. Default value: 1.

##### `tos_ceiling`

Data type: Optional[Integer[1]]

Specifies the ceiling tos option. Default value: 15.

##### `tos_cohort`

Data type: Variant[Boolean, Integer[0,1]]

Specifies the cohort tos option. Valid options: 0 or 1. Default value: 0.

##### `tinker`

Data type: Optional[Boolean]

Whether to enable tinker options. Default value: false.

##### `udlc`

Data type: Boolean

Specifies whether to configure NTP to use the undisciplined local clock as a time source. Default value: false.

##### `udlc_stratum`

Data type: Optional[Integer[1,15]]

Specifies the stratum the server should operate at when using the undisciplined local clock as the time source.
This value should be set to no less than 10 if ntpd might be accessible outside your immediate, controlled network.
Default value: 10.am udlc

##### `tos_maxclock`

Data type: Optional[Integer[1]]




### ntp::config


### ntp::install


### ntp::service


## Defined types

### ntp::qux

* **Since** 7.0.0

* **See also**
https://github.com/puppetlabs/puppet-strings


#### Examples
#####
```puppet
qux { 'blah':
  param1 => 'geese',
  param2 => false,
}
 ```


#### Parameters

The following parameters are available in the ntp::qux defined type.

##### `param1`

Data type: String

this is param1

Default value: 'ducks'
##### `param2`

Data type: Boolean

this is param2

Default value: false

## Resource types

### test
#### Examples
##### Using the type.
```puppet
Example { foo:
  Param => ‘hi’
}
```

#### Properties

The following properties are available in the test resource type.
##### `my_prop`

Valid values: foo, bar, baz

Documentation for a dynamic property.

##### `qux`

ok

#### Parameters

The following parameters are available in the test resource type.
##### `foo`

Is another metasyntactic variable

##### `my_param`

Valid values: value1, value2, value3

Documentation for a dynamic parameter.


## Functions

### dope

#### `dope(String $foo, Hash $opts, Optional[Array] $bars)`

overview string

Returns: `String` not a damn thing

##### `foo`

Data type: String

This is a string called foo

##### `bars`

Data type: Optional[Array]

This is an optional array called bars

##### `opts`

Data type: Hash

blah

### example

#### `example(String $name)`

An example function written in Pupppet.

Returns: `String` Returns a string.

##### `name`

Data type: String

The name to say hello to.
