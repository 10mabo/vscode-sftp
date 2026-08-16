# Changelog

All notable changes to this extension will be documented in this file.

## [1.0.0] - 2026-08-16

### Changed

- Forked the SFTP/FTP extension for independent development.
- Removed the `context` configuration option.
- Local temporary data is now stored in a hashed directory under `~/.sftp/tmp/`.
- Temporary directories are generated automatically from the connection configuration.
- Updated the extension documentation and configuration examples.
- Updated the extension name and display name for the independent Marketplace release.

### Fixed

- Improved handling of workspace-specific temporary directories.