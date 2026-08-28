# ImHex SDK Action

This is the official GitHub Action to setup the ImHex SDK for building ImHex plugins.

It sets up the toolchain (MSYS2 for Windows, Homebrew GCC for macOS) and downloads the SDK.

## Usage

### Setup an action

To use the action, simply add the following code to your CI script:

```yaml
- name: Install SDK
  id: install_sdk
  uses: WerWolv/imhex-download-sdk@v2
  with:
    imhex_version: '1.39.0'
```

Where the `imhex_version` input refers to the exact ImHex version whose SDK should be used.
For example, if you want to build a plugin for ImHex version 1.39.0, pass `1.39.0`.

Visit the [ImHex-Plugin-Template](https://github.com/WerWolv/ImHex-Plugin-Template) repository if you'd like to get started.

> [!IMPORTANT]
> ImHex 1.39.0 is not available yet.

#### ImHex 1.38.1 and older

ImHex versions older than `1.39.0` were based on the now deprecated MSYS2 MINGW64 when compiling for Windows. Newer releases use MSYS2 UCRT64 subsystem.

For compatibility please use an older version of this GitHub Action.

```yaml
- name: Install SDK
  id: install_sdk
  uses: WerWolv/imhex-download-sdk@vX.Y.Z
```

Where `@vX.Y.Z` refers to the ImHex version whose SDK should be used.
For example, if you want to build a plugin for ImHex version 1.38.1, use `WerWolv/imhex-download-sdk@v1.38.1`

### Inputs

All inputs and their defaults.

```yaml
- name: Install SDK
  id: install_sdk
  uses: WerWolv/imhex-download-sdk@v2
  with:
    # The version of SDK to install, e.g., "1.39.0", "latest" (default: latest)
    imhex_version: '1.39.0'
```

### Outputs

- `sdk_path` - Path to the ImHex SDK.


## License

This project is licensed under the terms of the [GPL-2.0-only license](https://github.com/WerWolv/imhex-download-sdk/blob/master/LICENSE).
