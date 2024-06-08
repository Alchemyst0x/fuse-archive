# fuse-archive

## Note

The only changes made to this fork of the [original repo](https://github.com/google/fuse-archive) are in [the Makefile](Makefile) and this [`README`](README.md) to enable compilation and usage on macOS. Specifically:

1. **Makefile Adjustments**:
   - Set [prefix](https://github.com/Alchemyst0x/fuse-archive/blob/main/Makefile#L5) to `/usr/local` to avoid read-only `/usr/bin`, and modified [`uninstall`](https://github.com/Alchemyst0x/fuse-archive/blob/main/Makefile#L29) to match.
   - [Ensured the use of `clang++`](https://github.com/Alchemyst0x/fuse-archive/blob/main/Makefile#L8) as the default compiler.
   - Added [macOS-specific flags](https://github.com/Alchemyst0x/fuse-archive/blob/main/Makefile#L11-L14) and [flags for C++ version compatibility](https://github.com/Alchemyst0x/fuse-archive/blob/main/Makefile#L9).

2. **README Updates**:
   - Added detailed installation instructions for macOS, including dependencies and environment variable setup.
   - Added usage examples and instructions for mounting archives with `fuse-archive`.

### Disclaimer

I am not affiliated with Google. See [the original README](https://github.com/google/fuse-archive/blob/main/README.md) for more information, and for anything else, please refer to [the canonical source codebase](https://github.com/google/fuse-archive/tree/main).

I am not responsible for any actions you take or any consequences that arise from using this code. Use it at your own risk.

---

## Installation Instructions for macOS

### Prerequisites

Ensure you have Homebrew installed. If not, you can install it by following the instructions at [brew.sh](https://brew.sh/).

### Dependencies

Install the required dependencies using Homebrew:

```sh
brew install libarchive macfuse pkg-config
```

### Building the Project

#### Clone the repository

```sh
git clone https://github.com/Alchemyst0x/fuse-archive.git && cd fuse-archive
```

Alternatively, if you'd rather clone the original repo and modify the Makefile yourself:

```sh
git clone https://github.com/google/fuse-archive.git && cd fuse-archive
```

#### Set the `PKG_CONFIG_PATH` environment variable

Locate `libarchive.pc` and add the directory containing this file to the `PKG_CONFIG_PATH` variable, e.g.:

```sh
find $(brew --prefix) -name libarchive.pc
# Output:
# /opt/homebrew/Cellar/libarchive/3.7.4/lib/pkgconfig/libarchive.pc
export PKG_CONFIG_PATH="/opt/homebrew/Cellar/libarchive/3.7.4/lib/pkgconfig:/usr/local/lib/pkgconfig"
```

#### Build the project

```sh
make all
```

### Installing the Binary

Install the binary to `/usr/local/bin`:

```sh
sudo make install
```

### Usage

Run the `fuse-archive` binary with the `-h` flag to see the usage instructions:

```sh
./out/fuse-archive -h
```

#### Example

For example, to mount a ZIP archive on a macOS system, you might do the following:

```sh
sudo fuse-archive -o allow_other /Users/YourUsername/some_zip_file.zip /Volumes/some_mounted_zip
```

You can then verify the mount was successful, e.g.:

```sh
ls /Volumes/some_mounted/zip
```

### Uninstalling

To uninstall the binary:

```sh
sudo make uninstall
```
