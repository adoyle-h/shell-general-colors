# Shell General Colors

A script to generate sets of shell variables (ANSI escape sequences) to control text color, boldness, underlining, blinking and other effects.

Support general colors: `BLACK` `RED` `GREEN` `YELLOW` `BLUE` `PURPLE` `CYAN` `WHITE` `GREY`.

Not support custom RGB color. [ansi][] is a good choice.  
So what difference between ansi and Shell General Colors? The main difference is the way to invoke.
Shell General Colors provides simple shell variables which aim to be fast in runtime while ansi provides flexible functions.

## TOC

<!-- MarkdownTOC GFM -->

- [Preview](#preview)
- [Installation](#installation)
- [Usage](#usage)
- [Advanced Usage](#advanced-usage)
    - [Change generated file path](#change-generated-file-path)
    - [Set variable prefix](#set-variable-prefix)
    - [Export escaped variables](#export-escaped-variables)
    - [Export both general variables and escaped variables](#export-both-general-variables-and-escaped-variables)
- [Suggestion, Bug Reporting, Contributing](#suggestion-bug-reporting-contributing)
- [Versioning](#versioning)
- [Copyright and License](#copyright-and-license)
- [References](#references)
- [Related Projects](#related-projects)

<!-- /MarkdownTOC -->

## Preview

See [Usage](#usage) and run `./test` to preview.

## Installation

```sh
# Clone this repo
git clone --recurse-submodules --depth 1 https://github.com/adoyle-h/shell-general-colors.git
```

## Usage

First, generate a colors.bash file to your project.

```sh
cd shell-general-colors
# "./generate -h" to get usage
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

echo -e "this is ${RED}red${RESET_ALL}. this is ${YELLOW}yellow${RESET_ALL}."
```

## Advanced Usage

### Change generated file path

```sh
./generate <file-path>
# <file-path> generated
```

### Set variable prefix

```sh
./generate -p C_
# C_BLACK, C_RED, C_BOLD_BLACK ...
```

### Export escaped variables

```sh
./generate -e _ESC
# BLACK_ESC, RED_ESC, BOLD_BLACK_ESC ...
```

You can use escaped variables with `cat`. For example,

```sh
cat <<EOF
this is ${RED_ESC}red${RESET_ALL_ESC}.
this is ${YELLOW_ESC}yellow${RESET_ALL_ESC}.
EOF
```

### Export both general variables and escaped variables

```sh
./generate -a -e _ESC
# BLACK, BLACK_ESC, RED, RED_ESC, BOLD_BLACK, BOLD_BLACK_ESC ...
```

## Suggestion, Bug Reporting, Contributing

Any suggestions and contributions are always welcome. Please open an [issue][] to talk with me.

## Versioning

See git [release tags][].

The versioning follows the rules of SemVer 2.0.0.

**Attentions**: anything may have **BREAKING CHANGES** at **ANY TIME** when major version is zero (0.y.z), which is for initial development and the public API should be considered unstable.

For more information on SemVer, please visit http://semver.org/.

## Copyright and License

Copyright (c) 2019 ADoyle. The project is licensed under the **BSD 3-clause License**.

See the [LICENSE][] file for the specific language governing permissions and limitations under the License.

See the [NOTICE][] file distributed with this work for additional information regarding copyright ownership.

## References

- [Wikipedia - ANSI escape code](https://www.wikiwand.com/en/ANSI_escape_code)
- [Stackoverflow - List of ANSI color escape sequences](https://stackoverflow.com/questions/4842424/list-of-ansi-color-escape-sequences)
- [FLOZz' MISC » bash:tip_colors_and_formatting](https://misc.flogisoft.com/bash/tip_colors_and_formatting)
- [ASCII Table - ANSI Escape sequences](http://ascii-table.com/ansi-escape-sequences.php)
- [ansi codes](https://bluesock.org/~willkg/dev/ansi.html#sequences)
- [vt100.net - ANSI Control Functions Summary](https://vt100.net/docs/vt510-rm/chapter4.html)
- [JAFROG'S DEV BLOG - Colors In Terminal](http://jafrog.com/2013/11/23/colors-in-terminal.html)

## Related Projects

- [lobash](https://github.com/adoyle-h/lobash): A collections of functions to enhance development efficiency.

<!-- links -->

[issue]: https://github.com/adoyle-h/shell-general-colors/issues
[release tags]: https://github.com/adoyle-h/shell-general-colors/releases
[LICENSE]: ./LICENSE
[NOTICE]: ./NOTICE
[ansi]: https://github.com/fidian/ansi
