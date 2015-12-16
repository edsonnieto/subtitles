# About

Subber is a cli tool and library for reading,
writing and manipulating .srt subtitle files written in Go

WARNING: The API is unstable, work in progress!

### Features

- Processes .srt and .ssa subtitles
- Cleans up the captions
- Optionally remove html tags or fix capitalization
- Outputs utf8 subtitle in the popular .srt format


### Why?

While VLC may swallow all kinds of malformed subtitles,
not all software are so forgiving.
So, sometimes "other software" needs a cleaned up .srt,
and the `subber` cli app automates this task.


# Installation

To install the command line:

```
go install github.com/martinlindhe/subber/cli/subber
```


# Usage

To download subtitles for a video file:

```
$ subber movie.mp4

Downloading subs for movie.mp4 ...
Cleaning sub movie.srt ...
Removing caption 82 [== sync, corrected by <font color="#00FF00">elderman</font> ==]
Written to movie.srt
```

Some additional flags (use `-h` for full list) includes:

  * `--keep-ads` do not remove advertising segments from the processesed sub
  * `--dont-touch` write sub as-is (downloaded are processed by default)`
  * `--skip-backups` by default, a .org file is created for every modified .srt
  * `--language="sv"` Specify another language, English subtitles is the default


Remove ads from an existing .srt file:

```
$ subber subtitle.srt

Removing caption 21 [<font color="#FFFF00"> Captions by VITAC  </font><font color="#00FFFF"> www.vitac.com</font>]
```

Strip html tags from .srt:

```
$ subber subtitle.srt --filter="html"

[html] <i>And there's a lot of it there.</i> -> And there's a lot of it there.
```

Normalize capitalization in .srt:

```
$ subber subtitle.srt --filter="caps"

[caps] INTRODUCING -> Introducing
[caps] right, to go? -> Right, to go?
```


# Contributing

Patches welcome!

Some ideas, in no particular order:

- automatically convert downloaded .ssa files to .srt
- filter: spell fixer
- filter: remove hearing aid tags [DOOR OPENS]
- make -v (verbose mode) have any effect


# See also

- [ssa2srt](https://github.com/martinlindhe/ssa2srt) for converting .ssa to .srt


# License

Under [MIT](LICENSE)
