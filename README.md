# Audacious - Patched Version

This is a custom build of the Audacious audio player with a critical fix for an assertion failure in the core library.

## Patched Fix: Tuple::set_int Assertion Failure

The original code contained a strict assertion in `src/libaudcore/tuple.cc` that would cause the player to crash (`SIGABRT`) when encountering certain malformed or unexpected metadata fields:

```cpp
assert(is_valid_field(field) && field_info[field].type == Int);
```

This has been replaced with a robust runtime check that logs an error message instead of crashing the application:

```cpp
if (!is_valid_field(field)) {
    AUDERR("Invalid field %d passed to set_int\n", field);
    return;
}
if (field_info[field].type != Int) {
    AUDERR("Field %d (%s) is not an Int field\n", field, field_info[field].name);
    return;
}
```

## Features

- **Crash Prevention**: Robust handling of metadata errors.
- **Improved Logging**: Errors are now reported via `AUDERR` for easier debugging.
- **Combined Package**: Specifically built with core and plugins for immediate use in Debian-based systems.

## Installation

You can install the pre-built patched package using:

```bash
sudo dpkg -i audacious-4.4-patched-with-plugins_amd64.deb
sudo ldconfig
```

Run with:
```bash
LD_LIBRARY_PATH=/usr/local/lib audacious
```

---
*Maintained by Djagbley Emmanuel*
