# mp3dant

mp3dant is a command-line tool for identifying, analyzing, and "correcting" MP3 [ID3](https://en.wikipedia.org/wiki/ID3) metadata and organization based on a rule set.
It consists of a series of subcommands for each action.

## Commands

    mp3dant scan - executes `mp3dant parse` across all files in a directory and subdirectories, using the directory structure to provide potentially missing artists and albums
    mp3dant parse - reads an MP3 and outputs the existing ID3 metadata as JSON
    mp3dant convert - Converts ID3 metadata from a provided rule set
    mp3dant write - writes a new MP3 file with the updated ID3 metadata

# Requirements/Installation #

mp3dant is a [Go](http://www.golang.org) application and was written and tested with version 1.16.4. It depends on the [bogem/id3v2](https://github.com/bogem/id3v2) library to process the ID3 metadata and the [spf13/Cobra](https://github.com/spf13/cobra) CLI library. It currently does not support any alternate files formats (.flac, .m4a, etc.) but may eventually expand coverage.

## Installation

# Usage

Each command has additional documentation provided.

  * [mp3dant](docs/root.md)
  * [mp3dant scan](docs/scan.md)
  * [mp3dant parse](docs/parse.md)
  * [mp3dant convert](docs/convert.md)
  * [mp3dant write](docs/write.md)

# Testing

mp3dant uses [go test](https://golang.org/pkg/testing/) for testing.

# Contributing

Please use the GitHub Issues for the project for pull requests, to suggest features, or to identify bugs.

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
