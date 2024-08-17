# Node Upgrader and Version Manager

Upgrades to the latest version of Node, or manages more versions of Node on the same machine, supporting all platforms including RISC-V, as simple es `rustup`.

* Small. Written in `bash`, easily extensible.
* Fast. Downloads and unpacks pre-built binary builds.
* Portable. Writes only to the user home directory.
* Simple. Switches the version globally, no environment variable changes needed.
* Efficient. Just run `nodeup up`.

Platforms: `aix-ppc64`, `darwin-x64`, `darwin-arm64`, `linux-x64`, `linux-x64-musl`, `linux-arm64`, `linux-armv7l`, `linux-loong64`, `linux-ppc64le`, `linux-riscv64`, `linux-s390x`, `windows-x86`, `windows-x64`, `windows-arm64`.

## Getting Started

Make sure that you have `bash` 4 or newer and `curl` available, execute the following command:

    curl -fSs https://raw.githubusercontent.com/prantlf/nodeup/master/install.sh | bash

Install the latest version of Node, if it hasn't been installed yet:

    nodeup install latest

Upgrade both the installer script and the Node language, if they're not the latest versions, and delete the previously active latest version from the disk too:

    nodeup up

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

For example, with the Node 1.23.0 activated:

    /home/prantlf/.nodeup
      ├── 20.16.0  (another version)
      ├── 22.6.0   (linked to /home/prantlf/.node)
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

## Debugging

If you enable `bash` debugging, every line of the script will be printed on the console. You'll be able to see values of local variables and follow the script execution:

    bash -x nodeup ...

You can debug the installer too:

    curl -fSs https://raw.githubusercontent.com/prantlf/nodeup/master/install.sh | bash -x

## Contributing

In lieu of a formal styleguide, take care to maintain the existing coding style. Lint and test your code.

## License

Copyright (c) 2024 Ferdinand Prantl

Licensed under the MIT license.
