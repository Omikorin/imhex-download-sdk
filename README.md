# ImHex SDK Action

This is the official GitHub Action to setup the ImHex SDK for building ImHex plugins.

It sets up the toolchain (MSYS2 for Windows, Homebrew GCC for macOS) and downloads the SDK.

## Usage

### Setup an action

To use the action, simply add the following code to your CI script:

```yaml
- name: Setup SDK
  id: setup_sdk
  uses: WerWolv/imhex-download-sdk@v2
  with:
    version: '1.39.0'
```

Where the `version` input refers to the exact ImHex version whose SDK should be used.
For example, if you want to build a plugin for ImHex version 1.39.0, pass `1.39.0`.

Visit the [ImHex-Plugin-Template](https://github.com/WerWolv/ImHex-Plugin-Template) repository if you'd like to get started.

> [!IMPORTANT]
> ImHex 1.39.0 is not available yet.

#### Using a version file

If you want to manage the ImHex SDK version via a separate file without a need to update workflow and/or your environment, you can create a file called e.g.: `.imhex-version` with the desired version:

```text
1.39.0
```

then, read that file inside your CI job:

```yaml
- name: Read .imhex-version
  id: imhex-version
  run: |
    IMHEX_VERSION=$(cat .imhex-version | tr -d '\r\n')
    echo "IMHEX_VERSION=${IMHEX_VERSION}" >> "${GITHUB_OUTPUT}"

- name: Setup SDK
  id: setup_sdk
  uses: WerWolv/imhex-download-sdk@v2
  with:
    version: '${{ steps.imhex-version.outputs.IMHEX_VERSION }}'
```

#### ImHex 1.38.1 and older

ImHex versions older than `1.39.0` were based on the now deprecated MSYS2 MINGW64 when compiling for Windows. Newer releases use MSYS2 UCRT64 subsystem.

For compatibility please use an older version of this GitHub Action.

```yaml
- name: Setup SDK
  id: setup_sdk
  uses: WerWolv/imhex-download-sdk@vX.Y.Z
```

Where `@vX.Y.Z` refers to the ImHex version whose SDK should be used.
For example, if you want to build a plugin for ImHex version 1.38.1, use `WerWolv/imhex-download-sdk@v1.38.1`

### Inputs

All inputs and their defaults.

```yaml
- name: Setup SDK
  id: setup_sdk
  uses: WerWolv/imhex-download-sdk@v2
  with:
    # ImHex version to target (e.g., 1.39.0 or nightly)
    # required
    version: '1.39.0'

    # Target architecture (x86_64 or arm64)
    # default: 'x86_64'
    arch: 'x86_64'

    # Whether to install system dependencies via pacman/brew
    # If false, then you need to provide the following executables: unzip for Windows and 7zz (sevenzip in brew) for macOS
    # default: 'true'
    install_dependencies: 'true'

    # Cache the downloaded ImHex SDK
    # default: 'true'
    cache: 'true'
```

### Outputs

- `sdk_path` - Path to the ImHex SDK.

## License

This project is licensed under the terms of the [GPL-2.0-only license](https://github.com/WerWolv/imhex-download-sdk/blob/master/LICENSE).
