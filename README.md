# mp3dant #

mp3dant is a command-line tool for identifying, analyzing, and "correcting" MP3 ID3 tags and organization based on a rule set.
It consists of a series of subcommands for each action.

## Commands

    mp3dant ingest - reads in a directory or directories and potentially uses that metadata in conjunction with the MP3's existing ID3 tags
    mp3dant parse - reads an MP3 and outputs JSON of the existing metadata
    mp3dant convert - applies a rule set against the MP3's metadata to convert the existing ID3 data as necessary
    mp3dant write - writes a new MP3 file with the updated ID3 data

# Requirements/Installation #

mp3dant is a [Go](http://www.golang.org) application and was written and tested with version 1.16.4. It depends on the https://github.com/bogem/id3v2 library to process the ID3 tags. It currently does not support any alternate files formats (.flac, .m4a, etc.) but may eventually expand coverage.

## Installation

# Usage

HOW DOES iTUNES LIKE HAVING FILES CHANGED FROM UNDER IT?
ANALYZE THE iTunes Library.xml as a potential output DIFF format (FUCK XML)
PERHAPS PARSE FROM IT TO FIX ID3 TAGS?
DOES iTUNES FIX ID3s?
HASH THE FILES, PUT HASH IN ID3 as METADATA?

Please use the GitHub Issues for the project to suggest features or to identify bugs.


# Usage #

CARGO CULT RUBOCOP's SYNTAx
YAML

```mp3dant```
With no arguments, mp3dant will output the help options.

```mp3dant scan```
Reads in the current directory, defaults to recursive.

```mp3dant dryrun```
Show what actions will be performed


#### -c/--config ####
rules file for processing

## --debug ##
This provides additional verbose debugging messages.

## -h/--help ##
Print the currently-supported usage options for mp3dant.

## --norecursive
Do not scan subdirectories

## -v/--version ##
Print the version of mp3dant currently installed.

## scan ##

### options ###

#### -d/--directory ####

#### -o/--output ####
file to output results

## fix

#### -o/--output ####
directory to output results
assumption is artist/album/

# Rules #
Crib from rubocop for syntax examples
Parse individual files first and then compare to others in the same directory as well.
Show the plan, it may fix issues in the groups
Each rule a separate file, to make adding new rules simple.
Base Rule providing mixins

## album artist ##
If missing, update the album artist to match the artist

## albums directories ##
Move files into album directories below the artist directory if unsorted

## artist directories ##
Move files into artist directories if unsorted

## case match ##
Identify within a directory mis-matched case of tags (ie. "Sonic Youth" vs. "sonic youth")

## duplicates ##
Identify tracks that appear to be duplicates. Show metadata differences.

## file rename ##
Rename files to the format "NUMBER NAME.mp3". Eventually may want to expose a --format for this.

## ID3v2 upgrade ##
Update ID3 tags from v1 to v2 (WHY)

## mismatched "The" ##
If a  artist may be called with the prefix "The", standardize listings (ie. "Beatles" vs. "The Beatles").

## missing ##
Identify missing tags

## missing files ##
If there is a sequence of tracks and any are missing, list them.

## number ##
If the filename starts with a number, does it match the ID3 track number?


# Testing #

mp3dant uses [XXX](http://rspec.info/) for testing. You should run the following before commiting.

    $ rspec test

The regression suite is a set of "bad" MP3s and a fix suite.
mp3 for each cop
output validated


[![Build Status](https://travis-ci.org/mattray/spiceweasel.png)](https://travis-ci.org/mattray/spiceweasel)
[![Code Climate](https://codeclimate.com/badge.png)](https://codeclimate.com/github/mattray/spiceweasel)

# Description #

id3cop scans a set of MP3s and attempts to identify inconsistencies in their ID3 tags based on the files and the directory structures. id3cop is inspired by the syntax of Rubocop. id3cop only works with ID3v2? MP3s are expected to be sorted by ARTIST/ALBUM/track.mp3

The [CHANGELOG.md](https://github.com/mattray/spiceweasel/blob/master/CHANGELOG.md) covers current, previous and future development milestones and contains the features backlog.

# Requirements #

id3cop uses XXX ID3 library. It is built and tested on MacOS and Linux?

# Rubocop Syntax #

Read in the ID3 tags of everything in the folder.
If there is case-insensitivity between Album, Artist, Album Artist or multiple versions of the same track FLAG

SKIP if there are multiple artists
If the Artist is set but not the Album artist, set the album artist to match

$ rubocop --help
Usage: rubocop [options] [file1, file2, ...]
    -L, --list-target-files          List all files RuboCop will inspect.
        --except [COP1,COP2,...]     Disable the given cop(s).
        --only [COP1,COP2,...]       Run only the given cop(s).
    -c, --config FILE                Specify configuration file.
        --auto-gen-config            Generate a configuration file acting as a
                                     TODO list.
        --exclude-limit COUNT        Used together with --auto-gen-config to
                                     set the limit for how many Exclude
                                     properties to generate. Default is 15.
        --force-exclusion            Force excluding files specified in the
                                     configuration `Exclude` even if they are
                                     explicitly passed as arguments.
        --force-default-config       Use default configuration even if configuration
                                     files are present in the directory tree.
        --no-offense-counts          Do not include offense counts in configuration
                                     file generated by --auto-gen-config.
    -f, --format FORMATTER           Choose an output formatter. This option
                                     can be specified multiple times to enable
                                     multiple formatters at the same time.
                                       [p]rogress (default)
                                       [s]imple
                                       [c]lang
                                       [d]isabled cops via inline comments
                                       [fu]ubar
                                       [e]macs
                                       [j]son
                                       [h]tml
                                       [fi]les
                                       [o]ffenses
                                       [w]orst
                                       custom formatter class name
    -o, --out FILE                   Write output to a file instead of STDOUT.
                                     This option applies to the previously
                                     specified --format, or the default format
                                     if no format is specified.
        --fail-level SEVERITY        Minimum severity (A/R/C/W/E/F) for exit
                                     with error code.
        --show-cops [COP1,COP2,...]  Shows the given cops, or all cops by
                                     default, and their configurations for the
                                     current directory.
    -F, --fail-fast                  Inspect files in order of modification
                                     time and stop after the first file
                                     containing offenses.
    -d, --debug                      Display debug info.
    -D, --display-cop-names          Display cop names in offense messages.
    -E, --extra-details              Display extra details in offense messages.
    -S, --display-style-guide        Display style guide URLs in offense messages.
    -l, --lint                       Run only lint cops.
    -a, --auto-correct               Auto-correct offenses.
    -n, --[no-]color                 Force color output on or off.
    -v, --version                    Display version.
    -s, --stdin                      Pipe source from STDIN.
                                     This is useful for editor integration.

## --cluster-file ##

Specify the file to use to override the `nodes` and `clusters` from the primary manifest file. This allows you to switch the target destination of infrastructure by picking different `--cluster-file` endpoints.

## --debug ##

This provides verbose debugging messages.

## -d/--delete ##

The `delete` option will generate the knife commands to delete the infrastructure described in the manifest. This includes each cookbook, environment, role, data bag and node listed. Node deletion will specify individual nodes and their clients, and attempt to pass the list of nodes to the cloud provider for deletion, and finish with `knife node bulk delete`. If you are mixing individual nodes with cloud provider nodes it is possible that nodes may be missed from cloud provider deletion and you should double-check (ie. `knife ec2 server list`). Some knife plugins do not use the node name as the ID, so they may fail at deletion (knife-rackspace for example).

## -e/--execute ##

The `execute` option will directly execute the knife commands, creating (or deleting or rebuilding) the infrastructure described in the manifest.

## --extractlocal ##

When run in a chef repository, this will print the knife commands to be run.

## --extractjson ##

When run in a chef repository, this will print a new JSON manifest that may be used as input to spiceweasel.

## --extractyaml ##

When run in a chef repository, this will print a new YAML manifest that may be used as input to spiceweasel.

## -h/--help ##

Print the currently-supported usage options for id3cop.

## --node-only ##

Loads from JSON or creates nodes on the server without bootstrapping, useful for pre-creating nodes. If you specify a run list with the node, it will override any run list specified within the JSON file.

## --novalidation ##

Disable validation ensuring existence of the cookbooks, environments, roles, data bags and nodes in infrastructure file.

## --parallel ##

Use the GNU 'parallel' command to execute 'knife VENDOR server create' commands that may be run simultaneously.

## -r/--rebuild ##

The rebuild option will generate the knife commands to delete and recreate the infrastructure described in the manifest. This includes each cookbook, environment, role, data bag and node listed.

## --siteinstall ##

Use the 'install' command with 'knife cookbook site' instead of the default 'download'.

## -v/--version ##

Print the version of spiceweasel currently installed.

# File Syntax #

Inspired by Rubocop's ``.rubocop.yml`` YAML file, the ``.id3cop.yml`` allows for the specification of the rules to enable and disable and which files to work with.

```
AllCops:
  Includes:
    - bin/**/*
    - lib/**/*
    - spec/**/*
  Excludes:
    - test/chef-repo/**/*
    - test/examples/**/*
    - test/extract-repo/**/*

# ignore long classes
ClassLength:
  Enabled: false

# ignore long lines
LineLength:
  Enabled: false

# Allow small arrays before forcing  %w or %W
WordArray:
  MinSize: 3

# Ignore this for now
MethodLength:
  Max: 125

# validation requires other objects
ParameterLists:
  Enabled: false

# this needs to be cleaned up in lib/spiceweasel/nodes.rb
BlockNesting:
  Enabled: false

RedundantReturn:
  # When true allows code like `return x, y`.
  AllowMultipleReturnValues: true
```

# License and Author #

|                      |                                       |
|:---------------------|:--------------------------------------|
| **Author**           |  Matt Ray (<mp3dant@mattray.dev>)     |
|                      |                                       |
| **Copyright**        |  Copyright (c) 2021, Matt Ray         |

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
