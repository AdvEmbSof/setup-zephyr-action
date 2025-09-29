# Setup Zephyr Environment Action

This GitHub Action installs the [Zephyr SDK](https://docs.zephyrproject.org/latest/develop/toolchains/zephyr_sdk.html) and sets up the environment for building Zephyr applications in CI.

It configures toolchains, exports environment variables like `ZEPHYR_BASE`, 
and prepares a west workspace for building and testing.

## Inputs
- `sdk_version`: Zephyr SDK version (default: `0.17.0`)
- `toolchains`: Space-separated toolchains (default: `arm-zephyr-eabi x86_64-zephyr-elf`)
- `path_west_workspace`: Path to use as west workspace root
- `path_west_manifest`: Path to the directory containing the manifest file

## Usage
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: <your-username>/setup-zephyr@v1
        with:
          sdk_version: "0.17.0"
          toolchains: "arm-zephyr-eabi"
          path_west_workspace: ${{ github.workspace }}
          path_west_manifest: ${{ github.workspace }}/manifest-repo/west.yml

      - run: west build -b nrf52840dk_nrf52840 samples/hello_world
```