Factorio Blueprint Decoder
==========================

## About

TL;DR: Decode [Factorio]'s binary `blueprint-storage.dat` into a blueprint-book
(in JSON format) for improved version control and other processing.

Players of [Factorio] can create "blueprints" which make it easier to store
plans of sections of their factory for later reuse. These blueprints are
stored either in the game's save file or in a separate file
`blueprint-storage.dat`. The latter contains the player's "personal" blueprints
which are available in every game.

This project decodes `blueprint-storage.dat` and creates a JSON file which
-- after some packing -- can be read back into Factorio via "Import String".

The JSON file can be stored in version-control providing some insight
what was changed. The binary format can be stored but provides no insight.

The JSON format is also open for more manipulation like merging two files or giving
another player a set of blueprints.

**Further** This project can also be a helpful base for decoding the `level.dat`
parts of a save file.

[Factorio]: https://factorio.com/

## Supported versions & mods

Usually only stable versions of the game are supported. Currently these are:

 - **1.0.0**: All vanilla stuff should work but using mods might turn up yet unknown fields.

 - **1.1.19**: Same as above but new entities like linked chests and linked belt are "Work In Progress".

Blueprints containing stuff from removed mods are currently also not supported.

## Usage

Basic Unix/Linux commandline knowledge is assumed :-)

The script requires [Python] 3.6 (or higher) installed.

`decode` converts a `*.dat` file into JSON:

	./decode tests/v1.0.0/bps-pipes.dat > /tmp/bps-pipes.json

`encode-export-string` converts JSON into a packed import/export string:

	./encode-export-string < /tmp/bps-pipes.json > /tmp/bps-pipes.export

That import/export string can be read back into Factorio using the command
"import string". The easiest way is to write the string into the clipboard
and paste it into the dialog:

	xclip -selection clipboard < /tmp/bps-pipes.export

[Python]: https://www.python.org/
