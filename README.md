# Shell General Colors

A script to generate sets of shell variables (ANSI escape sequences) to control text color, boldness, underlining, blinking and other effects.

Support general colors: `BLACK` `RED` `GREEN` `YELLOW` `BLUE` `PURPLE` `CYAN` `WHITE` `GREY`.

Not support custom RGB color. [ansi][] is a good choice.  
So what difference between ansi and Shell General Colors? The main difference is the way to invoke.
Shell General Colors provides simple shell variables which aim to be fast in runtime while ansi provides flexible functions.

## TOC

<!-- MarkdownTOC GFM -->

- [Preview](#preview)
- [Versioning](#versioning)
- [Installation](#installation)
- [Usage](#usage)
- [Advanced Usage](#advanced-usage)
    - [Change generated file path](#change-generated-file-path)
    - [Set variable prefix](#set-variable-prefix)
- [Suggestion, Bug Reporting, Contributing](#suggestion-bug-reporting-contributing)
- [Copyright and License](#copyright-and-license)

<!-- /MarkdownTOC -->

## Preview

See [Usage](#usage) and run `./test` to preview.

## Versioning

No version yet.

The versioning follows the rules of SemVer 2.0.0.

**Attentions**: anything may have **BREAKING CHANGES** at **ANY TIME** when major version is zero (0.y.z), which is for initial development and the public API should be considered unstable.

For more information on SemVer, please visit http://semver.org/.

## Installation

```sh
# Clone this repo
git clone --recurse-submodules --depth 1 https://github.com/adoyle-h/shell-general-colors.git
```

## Usage

First, generate a colors.bash file to your project.

```sh
cd shell-general-colors
./generate
# Generated file: colors.bash
```

The generated file "colors.bash" will contain below codes.

```sh
# General Foreground Colors
BLACK='\e[30m'
RED='\e[31m'
GREEN='\e[32m'
YELLOW='\e[33m'
BLUE='\e[34m'
PURPLE='\e[35m'
CYAN='\e[36m'
WHITE='\e[37m'
GREY='\e[90m'

# ...

# RESET
RESET_FG='\e[39m'
RESET_BG='\e[49m'
RESET_ALL='\e[0m'
```

Then source the colors.bash file and use these variables directly.

```sh
source <path>/colors.bash

echo -e "this is ${RED}red${RESET_ALL}. this is ${YELLOW}yellow"
```

## Advanced Usage

### Change generated file path

```sh
./generate <file-path>
# <file-path> generated
```

### Set variable prefix

```sh
PREFIX=C_ ./generate
# C_BLACK, C_RED, C_BOLD_BLACK ...
```

## Suggestion, Bug Reporting, Contributing

Any suggestions and contributions are always welcome. Please open an [issue][] to talk with me.

## Copyright and License

Copyright (c) 2019 ADoyle. The project is licensed under the **BSD 3-clause License**.

See the [LICENSE][] file for the specific language governing permissions and limitations under the License.

See the [NOTICE][] file distributed with this work for additional information regarding copyright ownership.


<!-- links -->

[issue]: https://github.com/adoyle-h/shell-general-colors/issues
[LICENSE]: ./LICENSE
[NOTICE]: ./NOTICE
[ansi]: https://github.com/fidian/ansi
