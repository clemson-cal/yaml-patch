# yaml-patch

Merge `serde_yaml::Value`'s together to enable hierarchical configurations

## Purpose

This crate extends any type which implements `serde::Serialize` and `serde::Deserialize` with four additional methods:

- `patch_from_value`
- `patch_from_str`
- `patch_from_reader`
- `patch_from_key_val`

For example, given a type

```rust
#[derive(Serialize, Deserialize)]
struct Configuration {
   a: f64,
   b: String,
}
```

you can update the data members of an instance from a `serde_yaml::Value::Mapping` with optional keys `"a"` or `"b"`. You can also patch an instance from a file (or anything `std::io::Read`) with valid YAML content:

```rust
let file = File::open("config.yaml")?;
config.patch_from_reader(file)?;
```

The crate also supports a key-path style YAML sytax syntax extension: for example

```rust
event.patch_from_key_val("date.year=2021")?;
```


## Usage

Add the following to your _Cargo.toml_:
```toml
[dependencies]
yaml-patch = "*"
```
