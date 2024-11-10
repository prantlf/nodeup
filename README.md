# Node Upgrader and Version Manager

Upgrades to the latest version of Node, or manages more versions of Node on the same machine, supporting all platforms including RISC-V, as simple es `rustup`.

* Small. Written in `bash`, easily extensible.
* Fast. Downloads and unpacks pre-built binary builds.
* Portable. Writes only to the user home directory.
* Simple. Switches the version globally, no environment variable changes needed.
* Efficient. Just run `nodeup up`.

Platforms: `aix-ppc64`, `darwin-x64`, `darwin-arm64`, `linux-x64`, `linux-x86`, `linux-x64-musl`, `linux-arm64`, `linux-armv6l`, `linux-armv7l`, `linux-loong64`, `linux-ppc64le`, `linux-riscv64`, `linux-s390x`, `windows-x86`, `windows-x64`, `windows-arm64`.

## Getting Started

Make sure that you have `bash` 4 or newer and `curl` available, execute the following command:

    curl -fSs https://raw.githubusercontent.com/prantlf/nodeup/master/install.sh | bash

Install the latest LTS version of Node, if it hasn't been installed yet:

    nodeup install lts

Before you continue, make sure that you have the following tools available: `curl`, `grep`, `jq`, `ln`, `rm`, `rmdir`, `sed`, `tar` (non-Windows), `uname`, `unxz` (non-Windows), `unzip` (Windows). It's likely that `jq` will be missing. You can install it like this on Debian: `apt-get install -y jq`.

Upgrade both the installer script and the Node language (to the latest LTS version), if they're not up-to-date, and delete the previously active latest LTS version from the disk too:

    nodeup up lts

If you specify `latest` instead of `'lts`, the latest non-LTS version will apply. The latest LTS version is 22.

## Installation

Make sure that you have `bash` 4 or newer and `curl` available, execute the following command:

    curl -fSs https://raw.githubusercontent.com/prantlf/nodeup/master/install.sh | bash

Both the `nodeup` and `node` should be executable in any directory via the `PATH` environment variable. The installer script will modify the RC-file of the shell, from which you launched it. The following RC-files are supported:

    ~/.bashrc
    ~/.zshrc
    ~/.config/fish/config.fish

If you use other shell or more shells, update the other RC-files by putting both the installer directory and the Node binary directory to `PATH`, for example:

    $HOME/.nodeup:$HOME/.node/bin:$PATH

Start a new shell after the installer finishes. Or extend the `PATH` in the current shell as the instructions on the console will tell you.

## Locations

| Path        | Description                                              |
|:------------|:---------------------------------------------------------|
| `~/.nodeup` | directory with the installer script and versions of Node |
| `~/.node`   | symbolic link to the currently active version of Node    |

For example, with the Node 20.16.0 activated:

    /home/prantlf/.nodeup
      ├── 20.16.0  (linked to /home/prantlf/.node)
      ├── 22.6.0   (another version)
      └── nodeup   (installer script)

## Usage

    nodeup <task> [version]

    Tasks:

      current              print the currently selected version of Node
      latest               print the latest version of Node for download
      local                print versions of Node ready to be selected
      remote               print versions of Node available for download
      update               update this tool to the latest version
      upgrade              upgrade Node to the latest and remove the current version
      up                   perform both update and upgrade tasks
      install <version>    add the specified or the latest version of Node
      uninstall <version>  remove the specified version of Node
      use <version>        use the specified or the latest version of Node
      help                 print usage instructions for this tool
      version              print the version of this tool

You can enter just `MAJ` or `MAJ.MIN` as `<version>`, instead of the full `MAJ.MIN.PAT`. When using the `install` or `use` tasks, the *most* recent full version that starts by the entered partial version will be picked. When using the `uninstall` task, the *least* recent full version that starts by the entered partial version will be picked.

## Debugging

If you enable `bash` debugging, every line of the script will be printed on the console. You'll be able to see values of local variables and follow the script execution:

    bash -x nodeup ...

You can debug the installer too:

    curl -fSs https://raw.githubusercontent.com/prantlf/nodeup/master/install.sh | bash -x

## Platform Detection

### Environment Variables

The following environment variables can be set before running `install.sh` or `nodeup`, if you know what you're doing:

| Variable       | Default value                 |
|:---------------|:------------------------------|
| `PLATFORM`     | detected using `uname`        |
| `OS`           | part of `PLATFORM` before `-` |
| `ARCH`         | part of `PLATFORM` after `-`  |
| `TOOL_URL_DIR` | https://nodejs.org/download/release or https://unofficial-builds.nodejs.org/download/release for platforms `linux-x86`, `linux-armv6l`, `linux-loong64`, `linux-riscv64` |
| `INST_DIR`     | `$HOME/.nodeup`               |
| `TOOL_DIR`     | `$HOME/.node`                 |

### ARM Architectures

The detection of the architecture ARM v6 and v7 may not work in your environment. For example, `uname -m` in Debian reports:

| Architecture | Output   |
|:-------------|:---------|
| ARM v6       | `armhf`  |
| ARM v7       | `armhf`  |
| ARM v8       | `arm64`  |

While, `uname -m` in Raspbian reports:

| Architecture | Output    |
|:-------------|:----------|
| ARM v6       | `armhf`   |
| ARM v7       | `armv7l`  |
| ARM v8       | `aarch64` |

`nodeup` regognises `armhf` as ARM v6. If you use it on Debian and ARM v7, enforce the proper architecture by setting the environment variable `ARCH` explicitly:

    ARCH=armv7l nodeup ...

If you don't do it, the `node` executable will work well nevertheless, because binaries for ARM v6 can be run on ARM v7. Just the performance of floating point computations may be lower.

If `uname` reports other value than `armhf`, the platform recognition will work well. Pay attention to the console output, in particular to this line:

    detected platform linux-armv6l

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Lint and test your code.

## License

Copyright (c) 2024 Ferdinand Prantl

Licensed under the MIT license.
