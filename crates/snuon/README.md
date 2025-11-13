# SNUON - Stupid NUON

**WARNING: This is intentionally a broken/stupid version of NUON. It does NOT support round-tripping!**

SNUON is a serialization-only variant of NUON that removes all escaping. This makes it unsuitable for proper data serialization where you need to parse the output back, but can be useful for simple output where you don't want quotes or escaping.

## Why is it "stupid"?

SNUON is "stupid" because:
- It only does serialization (no deserialization/parsing)
- It removes all escaping from strings
- Quotes will not be escaped
- Special characters will not be escaped
- **You cannot parse SNUON output back into valid data structures**

This means you will lose data if you try to round-trip through SNUON:
```rust
// This will NOT work:
let data = value_to_snuon(my_value);
let parsed = from_nuon(data); // Will fail or produce wrong results!
```

## When might you use this?

Only use SNUON when:
- You need human-readable output that you'll never parse back
- You want to avoid escaped quotes in your output
- You understand the data loss implications

## Example

```rust
use snuon::to_snuon;

// Strings with quotes won't be escaped:
let val = Value::test_string("hello\"world");
let output = to_snuon(&engine_state, &val, ToStyle::Default, None, false)?;
// Output: hello"world (without escaping the quote)
```

For proper NUON support with round-tripping, use the `nuon` crate instead.
