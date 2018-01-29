# Reference
## Classes
* [`klass`](#klass): A simple class.
## Defined types
* [`definedtype`](#definedtype): A simple defined type.
## Resource types
* [`database`](#database): An example database server resource type.
## Functions
* [`func`](#func): A simple Puppet function.
* [`func4x`](#func4x): An example 4.x function.
* [`func4x_1`](#func4x_1): An example 4.x function with only one signature.
## Classes

### klass

The following parameters are available in the klass class.

##### `param1`

Data type: Integer

First param.

##### `param2`

Data type: Any

Second param.

##### `param3`

Data type: String

Third param.

Default value: hi

### Defined types

#### definedtype

The following parameters are available in the definedtype defined type.

##### `param1`

Data type: Integer

First param.


##### `param2`

Data type: Any

Second param.


##### `param3`

Data type: String

Third param.

Default value: hi

### Resource types

### database

The following attributes are available in the database resource type.

#### properties

##### `ensure`

Valid values: present, absent, up, down

Aliases:  up => present  down => absent

What state the database should be in.

Default value: up

##### `file`

The database file to use.

##### `log_level`

Valid values: debug, warn, error

The log level to use.

Default value: warn

#### parameters

##### `address`

namevar

The database server name.

##### `encryption_key`

The encryption key to use.

##### `encrypt`

Valid values: true, false, yes, no

Whether or not to encrypt the database.

Default value: false


## Functions

### func

#### `func(Integer $param1, Any $param2, String $param3 = hi)`

A simple Puppet function.
Returns: `Undef` Returns nothing.

##### `param1`

Data type: Integer

First param.

##### `param2`

Data type: Any

Second param.

##### `param3`

Data type: String

Third param.

### func4x

#### `func4x(Integer $param1, Any $param2, Optional[Array[String]] $param3)`

The first overload.
Returns: `Undef` Returns nothing.

##### `param1`

Data type: Integer

The first parameter.

##### `param2`

Data type: Any

The second parameter.

##### `param3`

Data type: Optional[Array[String]]

The third parameter.

#### `func4x(Boolean $param, Callable &$block)`


Returns: `String` Returns a string.

##### `param`

Data type: Boolean

The first parameter.

##### `&block`

Data type: Callable

The block parameter.

### func4x_1

#### `func4x_1(Integer $param1)`

An example 4.x function with only one signature.
Returns: `Undef` Returns nothing.

##### `param1`

Data type: Integer

The first parameter.
