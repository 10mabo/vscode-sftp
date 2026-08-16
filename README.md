# SFTP Sync Extension for VS Code

[**vscode-sftp**](https://github.com/10mabo/vscode-sftp)
forked from [Natizyskunk/vscode-sftp](https://github.com/Natizyskunk/vscode-sftp)

This is a fork of the VS Code SFTP extension. It contains modifications and fixes for my own development workflow.

The original project was itself forked from [liximomo/vscode-sftp](https://github.com/liximomo/vscode-sftp).

---

VSCode-SFTP enables you to edit remote files via SFTP or FTP.

It provides a familiar workflow for working with remote files directly from VS Code.

---

## Configuration

The extension is configured using a `sftp.json` file inside the `.vscode` directory of your workspace.

Create the configuration with:

```text
SFTP: config
```

A basic configuration looks like this:

```json
{
    "name": "My Server",
    "host": "example.com",
    "protocol": "sftp",
    "port": 22,
    "username": "username",
    "remotePath": "/var/www/project",
    "uploadOnSave": true
}
```

### Common Configuration Options

| Option           | Description                                   |
| ---------------- | --------------------------------------------- |
| `name`           | Name of the configuration                     |
| `host`           | Remote server hostname or IP address          |
| `protocol`       | Connection protocol: `sftp`, `ftp` or `local` |
| `port`           | Remote server port                            |
| `username`       | Username used for authentication              |
| `password`       | Password used for authentication              |
| `privateKeyPath` | Path to an SSH private key                    |
| `remotePath`     | Remote directory to synchronize               |
| `uploadOnSave`   | Upload the file automatically after saving    |
| `downloadOnOpen` | Download a file when it is opened             |
| `useTempFile`    | Use a temporary file during transfers         |
| `ignore`         | Files or directories to exclude               |
| `ignoreFile`     | Path to an ignore file                        |
| `watcher`        | Configuration for automatic file watching     |
| `profiles`       | Define multiple connection profiles           |
| `defaultProfile` | Profile selected by default                   |

### Upload on Save

To automatically upload files after saving:

```json
{
    "host": "example.com",
    "username": "username",
    "remotePath": "/var/www/project",
    "uploadOnSave": true
}
```

### File Watcher

The File Watcher can automatically upload changed files and remove deleted files from the remote server.

```json
{
    "host": "example.com",
    "username": "username",
    "remotePath": "/var/www/project",
    "watcher": {
        "files": "**/*",
        "autoUpload": true,
        "autoDelete": true
    }
}
```

The watcher is optional.

### Profiles

Profiles allow multiple server configurations to be stored in one `sftp.json`:

```json
{
    "username": "username",
    "remotePath": "/var/www/project",

    "profiles": {
        "development": {
            "host": "dev.example.com",
            "remotePath": "/var/www/dev",
            "uploadOnSave": true
        },

        "production": {
            "host": "prod.example.com",
            "remotePath": "/var/www/prod",
            "uploadOnSave": false
        }
    },

    "defaultProfile": "development"
}
```

Use:

```text
SFTP: Set Profile
```

to switch between profiles.

### Temporary Files

The extension uses a temporary local directory for each remote connection.

The directory is created automatically based on the connection configuration.

On macOS and Linux, the files are stored under:

```text
~/.sftp/tmp/<hash>/
```

On Windows, the corresponding directory is located under the user's home directory:

```text
%USERPROFILE%\.sftp\tmp\<hash>\
```

The `<hash>` is generated from the following connection settings:

* `protocol`
* `host`
* `port`
* `username`
* `remotePath`

This ensures that different remote configurations use separate local directories.

The temporary directory does not need to be configured manually.

### Important: `context`

The `context` configuration option from the original extension has been removed from this fork.

The local base directory is determined automatically from the VS Code workspace and the SFTP configuration.

Therefore, existing configurations containing:

```json
"context": "some/path"
```

should remove this option.

For example, use:

```json
{
    "host": "example.com",
    "username": "username",
    "remotePath": "/var/www/project"
}
```

instead of:

```json
{
    "context": "project",
    "host": "example.com",
    "username": "username",
    "remotePath": "/var/www/project"
}
```

### Remote Explorer

The Remote Explorer uses the workspace and the configured `remotePath` to determine the corresponding remote location.

No `context` setting is required.

---

## Development

### Compile

Compile the extension from the project directory:

```bash
npm run compile
```

The command should complete without errors.

### Test the Extension in VS Code

1. Open the project in VS Code.
2. Compile the extension:

```bash
npm run compile
```

3. Press:

```text
Fn+F5
```

This opens a new **Extension Development Host** window.

The extension running in this window is the local development version.

After making changes to the source code, compile again and restart the debug session as necessary.

### Build a VSIX

Install `vsce` if it is not already installed:

```bash
npm install -g @vscode/vsce
```

Then create the VSIX package:

```bash
vsce package
```

A file similar to this will be created:

```text
vscode-sftp-1.0.0.vsix
```

The `.vsix` file can be installed through:

```text
Extensions: Install from VSIX...
```

---

## Installation from VSIX

To install a locally built VSIX:

1. Open Extensions in VS Code (`Ctrl+Shift+X` / `Cmd+Shift+X` on macOS).
2. Open the **...** menu.
3. Select **Install from VSIX...**.
4. Select the generated `.vsix` file.
5. Reload VS Code if requested.

---

## Original Project

This fork is based on:

[Natizyskunk/vscode-sftp](https://github.com/Natizyskunk/vscode-sftp)

The Natizyskunk project was itself forked from:

[liximomo/vscode-sftp](https://github.com/liximomo/vscode-sftp)

This fork is maintained primarily for my personal development workflow.

---

## License

This project is based on the original `liximomo/vscode-sftp` project.

See [LICENSE](LICENSE) for the applicable license.
