# Pixel perfect Twemoji for Minecraft: Java Edition
This resource pack adds all of Twemoji, redrawn by hand as pixel art
at 9x9 pixels, to the default font in Minecraft: Java Edition
version 1.16 or later.


## Installation
Please download the .zip file from the releases section, put it in your
resource packs folder and select it for use in-game.

You can also embed this pack into another pack,
for use on a server or custom world for example.
Please remember to credit the project as it is
one of the requirements of the project license.


## Basic usage 
Most standard emoji characters will just work if you copy and paste them in or
use some kind of emoji input. For example, try copying emoji from
[this site](https://emojifinder.com/) or using the Windows emoji picker (`Win+.`).

However, emoji that consist of sequences of multiple character are not supported
by vanilla and will show up as multiple, separate characters. Sorry.
See below for ways to develop around this.


## Remapped characters (for developers)
In order to have any support for emoji consisting of sequences they have been
remapped to unused single characters. An index of these can be found in
[/assets/emoji_remappings/lang/en_us.json](assets/emoji_remappings/lang/en_us.json).

For example, `\ud83d\udc69\u200d\ud83d\udd2c` (👩+🔬=👩‍🔬)
is mapped to `\udb80\udf30` using this translation snippet:

```json
"\ud83d\udc69\u200d\ud83d\udd2c": "\udb80\udf30"
```

**Please note that vanilla has no mechanism to
automatically convert to the remapped form.**
A custom emoji picker or some kind of mod/plugin is
required to make using these a smooth experience. 

Because the index acts as a language file, a server side chat listener
could detect emoji sequences and turn them into translations like this one:

```json
{"translate": "\ud83d\udc69\u200d\ud83d\udd2c"}
``` 

Any client with the pack installed can then perform the remapping for the server.
If the pack is not installed or the sequence is not found then it will just
fall back to displaying the sequence. This means that the server doesn't need a
complete list of emoji sequences, just a way to detect potential ones.

(The [Unicode website](https://unicode.org/Public/emoji/latest/)
contains data files describing what is an emoji.)


## Shortcodes (for developers)
Shortcodes are a popular way to insert emoji by name. An index of shortcodes
can be found in [/assets/emoji_shortcodes/lang/en_us.json](assets/emoji_shortcodes/lang/en_us.json).

For example, `:thinking:` is mapped to `\ud83e\udd14` (🤔):

```json
"thinking": "\ud83e\udd14"
```

Emoji that need remapping already map to the remapped version.

**Please note that vanilla has no mechanism to
automatically convert shortcodes into emoji.**
Some kind of mod/plugin is required.

Because the index acts as a language file, a server side chat listener could
detect shortcodes and turn them into translations like this one:

```json
{"translate": ":thinking:"}
``` 

Any client with the pack installed can then convert it for the server. If the
pack is not installed or the shortcode is not found then it will just fall back
to displaying the shortcode. This means that the server doesn't need a complete
list of shortcodes, just a way to detect potential ones by finding substrings
beginning and ending with a colon `:`.


### Custom emoji?
Custom emoji could be created in a similar way by adding them to unused code
points of the default font and adding a translation with a shortcode.
For example, this translation snippet adds the shortcode `:pog:` for the
character `\uE502`:

```json
":pog:": "\uE502"
```

## Reverse shortcodes (for developers)
Maybe you want to display a name for each emoji, in some hover text for example.
That is where reverse shortcodes come in. An index of these can be found in
[/assets/emoji_shortcodes_reverse/lang/en_us.json](assets/emoji_shortcodes_reverse/lang/en_us.json).

For example, `\u200c\ud83e\udd14` (`‌` + 🤔) is mapped to `:thinking:` using
this translation snippet:

```json
"\u200c\ud83e\udd14": ":thinking:"
```

`\u200c` is added to each entry to allow the index to be used as a language file
without conflicting with the other indexes. If the pack is not installed or the
emoji is not found then it will just fall back to displaying the characters,
including the invisible `\u200c`.

A server side chat listener could detect shortcodes and
turn them into emoji with tooltips like this one:
```json
{"translate": ":thinking:", "hoverEvent": {"action": "show_text", "contents": ":thinking:"}}
```

With reverse shortcodes, it could also detect emoji and
emoji sequences and also give them tooltips like this one:
```json
{"translate":"\ud83e\udd14","hoverEvent":{"action":"show_text","contents":{"translate":"%1851878757$s\ud83e\udd14"}}}
```


## License
Graphics based on Twemoji Copyright (c) 2018 Twitter, Inc and other contributors, licensed under Creative Commons Attribution 4.0 International

Pixel art and resource pack adaptation Copyright (c) 2020 Amber, licensed under Creative Commons Attribution 4.0 International
