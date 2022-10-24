# Shell General Colors

A script to generate sets of shell variables (ANSI escape sequences) to control text color, boldness, underlining, blinking and other effects.

Support general colors: `BLACK` `RED` `GREEN` `YELLOW` `BLUE` `PURPLE` `CYAN` `WHITE` `GREY`.

Not support custom RGB color. [ansi][] is a good choice.

The difference between ansi and Shell General Colors is usability.
Shell General Colors provides simple variables which aim to be fast in runtime while ansi provides flexible functions.

## Preview

See [Usage](#usage) and run `./test` to preview.

## Installation

```sh
# Clone this repo
git clone --depth 1 https://github.com/adoyle-h/shell-general-colors.git
# Copy it to somewhere in your path
sudo ln -s "$PWD/generate" /usr/local/bin/shell-general-colors
```

## Usage

There are two ways to generate colors: list or map.

### Color List
#### Generate Color List

First, generate a colors.bash file to your project.

```sh
# cd to your project
# "shell-general-colors -h" to get usage
shell-general-colors
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

#### Use Color List

Then source the colors.bash file and use these variables directly.

```sh
source <path>/colors.bash

echo -e "this is ${RED}red${RESET_ALL}. this is ${YELLOW}yellow${RESET_ALL}."
printf 'this is %bblue%b.' "${BLUE}" "${RESET_ALL}"
```

If you want to use color variables with [here documents][]. Use [escaped variables](#export-escaped-variables).

### Color Map
#### Generate Color Map

First, generate a colors.bash file to your project.

```sh
# cd to your project
# "shell-general-colors -h" to get usage
shell-general-colors --map
# Generated file: colors.bash
```

The generated file "colors.bash" will contain below codes.

```sh
declare -g -A colors=(

  # General Foreground Colors
  [BLACK]='\e[30m'
  [RED]='\e[31m'
  [GREEN]='\e[32m'
  [YELLOW]='\e[33m'
  [BLUE]='\e[34m'
  [PURPLE]='\e[35m'
  [CYAN]='\e[36m'
  [WHITE]='\e[37m'
  [GREY]='\e[90m'

  # ...

  # RESET
  [RESET_FG]='\e[39m'
  [RESET_BG]='\e[49m'
  [RESET_ALL]='\e[0m'
)
```

#### Use Color Map

Then source the colors.bash file and use these variables directly.

```sh
source <path>/colors.bash

RESET_ALL=${colors[RESET_ALL]}
color1=RED
color2=YELLOW
color3=BLUE

echo -e "this is ${colors[color1]}red${RESET_ALL}. this is ${colors[color2]}yellow${RESET_ALL}."
printf 'this is %bblue%b.' "${colors[color3]}" "${RESET_ALL}"
```

If you want to use color variables with [here documents][]. Use [escaped variables](#export-escaped-variables).

## Advanced Usage

### Change generated file path

```sh
shell-general-colors "~/colors.bash"
# $output generated
```

### Force write

The script checks existed file by default. You can force write file with `-f` option.

```sh
shell-general-colors -f
# $output generated
```

### Set variable prefix

If `-p=<prefix>` set, Add prefix `<prefix>` to each name of exported variables.

```sh
shell-general-colors -p C_
# C_BLACK, C_RED, C_BOLD_BLACK ...
```

### Export escaped variables

If `-e` set, export escaped variables instead of general variables. 

If `-e=<escaped_suffix>` set, export escaped variables instead of general variables. And add suffix `<escaped_suffix>` to each name of escaped variables.

```sh
shell-general-colors -e _ESC
# BLACK_ESC, RED_ESC, BOLD_BLACK_ESC ...
```

You can use escaped variables with [here documents][]. For example,

```sh
cat <<EOF
this is ${RED_ESC}red${RESET_ALL_ESC}.
this is ${YELLOW_ESC}yellow${RESET_ALL_ESC}.
EOF
```

### Export both general variables and escaped variables

```sh
shell-general-colors -a -e _ESC
# BLACK, BLACK_ESC, RED, RED_ESC, BOLD_BLACK, BOLD_BLACK_ESC ...
```

## Suggestion, Bug Reporting, Contributing

Any suggestions and contributions are always welcome. Please open an [issue][] to talk with me.

## Versioning

See [releases][].

The versioning follows the rules of SemVer 2.0.0.

**Attentions**: anything may have **BREAKING CHANGES** at **ANY TIME** when major version is zero (0.y.z), which is for initial development and the public API should be considered unstable.

For more information on SemVer, please visit http://semver.org/.

## Copyright and License

Copyright 2019~2022 ADoyle (adoyle.h@gmail.com) Some Rights Reserved. The project is licensed under the **BSD 3-clause License**.

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

## Other Projects

[Other shell projects](https://github.com/adoyle-h?tab=repositories&q=&type=source&language=shell&sort=stargazers) created by me.

<!-- links -->

[issue]: https://github.com/adoyle-h/shell-general-colors/issues
[releases]: https://github.com/adoyle-h/shell-general-colors/releases
[LICENSE]: ./LICENSE
[NOTICE]: ./NOTICE
[ansi]: https://github.com/fidian/ansi
[here documents]: http://tldp.org/LDP/abs/html/here-docs.html
