# Protocol Buffers (Protobuf)

**Protocol Buffers (Protobuf)** is a versatile language- and platform-neutral format for data representation and serialization used for storage and transmission of structured records. It was developed by Google and made available to the broader community. The latest version as of 2022 is Proto3. Protocol buffers form the foundation for inter-service communication in Google's SOA called gRPC. Protocol buffers format has the benefit of being simple, concise and fast to process, at the expense of not being self-describing, unlike other formats used for similar purposes such as XML, JSON, etc. That is, protocol buffer data are represented in a dense binary form called **wire**, from which the field names are absent. In order to make a wire parsable, protobuf user must provide a description file, called **protobuf schema** that contains the description of the particular protobuf data being used in the system. Schemas are stored in schema files that have a `.proto` extension. A typical protobuf schema contains descriptions of one or more record-like structures called **protobuf message types** that contain one or more typed **fields**, which are name-value pairs defining and constraining the kind of data to be stored in that field. The exact syntax of the protocol buffer schema is specified by the **protocol buffers language**. Based on the .proto file with the schema for protobuf messages, language-specific parsers will generate the code to work with these protobufs, e.g., a protobuf parser for C++ will generate classes incapsulating message fields and methods to work with those fields, as well as necessary header files.

## Syntax
A typical protobuf file has the following structure:
```
syntax = "proto3";

message <MessageTypeName> {
    [field_rule] <field_type> <field_name> = <field_number>;
    [field_rule] <field_type> <field_name> = <field_number>;
    ...
    [field_rule] <field_type> <field_name> = <field_number>;    
}

...

message <MessageTypeName> {
    [field_rule] <field_type> <field_name> = <field_number>;
    [field_rule] <field_type> <field_name> = <field_number>;
    ...
    [field_rule] <field_type> <field_name> = <field_number>;    
}
```

For example, if we want to store and process records containing information about clients or employees, we can define the following message type:

```
message Person {
    string name = 1;
    int32 age = 2;
    string address = 3;
    string birthdate = 4;
    ...
}
```

Here, [field_rule] denotes an optional tag specifying the behaviour of the that field in the protobuf data. In proto3, the possible values are:
* `singular` - a message can contain zero or one instances of that field. This is the default rule that is assumed when no other field rules have been specified.
* `optional` - a message can contain zero or one instances of that field, but with this rule, it is possible to check whether the value was explicitly assigned or the default value for the field was used. The reason for this is that in proto3, some fields have default values, e.g., 0 for integers, that are assigned to the field if no value has been set explicitly. However, these default values are not represented when the message is parsed into the wire format (i.e., the defult values are dropped). But the same happens even if the field was explicitly set to the default value. So, from the standpoint of a receiving party, when the received wire does not contain a value for a particular field, it is impossible to say whether the field was not set at all, or it was set to a default value. `Optional` solves this problem by always adding explicitly set value to the wire. That is, if the field was assigned a value (default or not), it will be serialized, otherwise the field will not be serialized to the wire.
* `repeated` - a message can contain zero or more instances of that field. The order of the instances will be preserved after serialization.
* `map` - introduces a key-value map type.
  
Field types designate the type of data stored in that field, e.g., an integer, a string, etc. Protobuf types mostly correspond to the standard programming language type set, but there are a few aspects that should be kept in mind. The standard types in proto3 are:
* `int32, int64` - used to store standard 32-bit integers, but when parsed into wire format use variable-length encoding. These data formats are inefficient to representing negative numbers.
* `uint32, uint64` - variable-length encoded unsigned integers.
* `sint32, sint64` - variable-length encoded signed integers. These are more efficient at storing negative numbers.
* `fixed32, fixed64` - use fixed 4- and 8-byte representation for unsigned integers. More efficient than uint32, uint64 for large numbers ($>2^{28}, >2^{56}$).
* `sfixed32, sfixed64` - use fixed 4- and 8-byte representation for signed integers.
* `bool` - standard boolean values.
* `string` - a UTF-8-encoded string of length $\leq 2^{32}$.
* `byte` - arbitrary byte array of length $\leq 2^{32}$.
A note on the default value for the types. For numeric types, the default value is 0, for strings and byte arrays the defaults are, respectively, empty string and empty byte array. For booleans the default is `False`. For enum types, the default is the first defined enum value, which must always be set to 0. Finally, for the message fields, the behaviour depends on the exact language in which the protobuf is being used.

Field names are simply human-readable identifiers for the fields. They are dropped when the message is encoded in the binary format and are only present in the protobuf schema or human-friendly representations.

Finally, field numbers are unique positive integer identifiers that serve to demarcate the fields in the binary encoding of a protobuf message. They must be selected from the interval $[1, 2^{29}-1]$. Since field numbers are used for field identification during parsing of binary encoded protobufs, these numbers should not change for existing fields once the message specification is published. That said, new fields may be introduced, and vacant field numbers may be assigned to them. When choosing a field number for a particular field one needs to keep in mind a few considerations:
* Some field numbers are reserved. In particular:
  * Already assigned field numbers cannot be reused.
  * Field numbers in the range `[19000, 19999]` are reserved for Protocol Buffers parser use and cannot be used.
  * Field numbers that are explicitly reserved using `reserved` keyword cannot be used.
* Field numbers in the interval `[1, 15]` are encoded in one byte (the encoding combines the field number and the field type), field numbers in the interval `[16, 2047]` take two bytes. Using smaller fields numbers for the more frequent fields will help reduce the size of the binary encoding of the messages.

A few words on the `reserved` keyword. This keyword is used to prevent the use of some field names/numbers, e.g., in the case when the author deprecates an existing field, but wants to prevent the users from defining the field with the same name/number in the future, in order to avoid compatibility issue (data corruption, etc.). The syntax is as follows:
```
message MyMsg {
    reserved 3, 6, 10-20;
    reserved "abc", "foo", "baz";
}
```
Note that while one can reserve both names and field numbers, one cannot mix them in a single `reserve` statement.

Protobuf syntax supports C-style comments, i.e., use `//` for single-line and `/* ... */` for multiline comments.

If one wants to restrict the set of values that a particular field can assume, one can do this by introducing an enumeration type and listing all the possible values for the enumeration as numerical constants, e.g.,

```
enum ResidenceTypes {
    UNSPECIFIED = 0;
    APARTMENT = 1;
    SINGLE_FAMILY_HOME = 2;
    CONDOMINIUM = 3;
    OTHER = 4;
}

message Person {
    string name = 1;
    int32 age = 2;
    string address = 3;
    string birthdate = 4;
    ResidenceTypes residence_type = 5;
}
```

#Protobuf, #proto3