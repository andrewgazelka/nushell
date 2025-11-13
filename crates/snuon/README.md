Support for the SNUON format.

The SNUON format is a variant of NUON that uses raw strings instead of escape sequences.
All NUON features are supported:
- trailing commas are allowed
- commas are optional in lists
- quotes are not required around keys or any _bare_ string that do not contain spaces or special characters
- comments are allowed, though not preserved when using [`from_snuon`]

## Key Difference from NUON
SNUON uses Nushell's raw string syntax (r#'...'#) instead of escape sequences when outputting strings that contain quotes or special characters. This makes the output more readable and eliminates the need for escaping.

## Example
A string with quotes in NUON would be:
```nuon
"hello\"world"
```

The same string in SNUON would be:
```snuon
r#'hello"world'#
```

Raw strings can nest by using multiple `#` symbols:
```snuon
r##'This contains r#'nested raw strings'#'##
```
