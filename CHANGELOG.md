# Changelog - Audacious Patched

## [1.0.1] - 2025-12-30

### Fixed
- **Core (libaudcore):** Resolved a critical assertion failure in `Tuple::set_int`.
  - The strict `assert(is_valid_field(field) && field_info[field].type == Int)` was replaced with a robust runtime check.
  - Invalid field access or type mismatches now log a detailed error message (`AUDERR`) instead of crashing the application.
  - This prevents crashes when encountering malformed or unexpected metadata in files or plugins.

### Added
- **Packaging:** Created a combined Debian binary package (`audacious-4.4-patched-with-plugins_amd64.deb`) that includes:
  - The patched Audacious core.
  - A comprehensive set of Audacious plugins (compiled with essential dependencies).
- **Verification Walkthrough:** Added a [walkthrough](file:///home/ghost/.gemini/antigravity/brain/06c0bf85-afb1-49f6-9cab-b6aa0d260a73/walkthrough.md) for manual verification of the fix.

### Technical Details
- Modified file: `src/libaudcore/tuple.cc`
- New dependencies for build: `runtime.h` included in `tuple.cc` for logging.
- Build system: Configured with `autogen.sh` and `./configure`.
- Plugin configuration: Disabled `json-glib` and `neon` dependent plugins to match environment constraints while maintaining core functionality.
