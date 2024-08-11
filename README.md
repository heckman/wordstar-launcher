# wordstar-launcher

A tool to launch [_WordStar_](https://sfwriter.com/wordstar.htm) with [_DOSBox-X_](https://dosbox-x.com/) on _macOS_.

It works with a _WordStar 7_ archive that was put together by science-fiction writer Robert J. Sawyer. It can be downloaded from [his blog](https://sfwriter.com/blog/?p=5806).

The _DOS-Box-X_ emulator can be download from its [releases](https://github.com/joncampbell123/dosbox-x/releases) page on *GitHub*. The only version that has been tested is the `sdl2` version in the release named [`dosbox-x-macosx-arm64-20240702034526.zip`](https://github.com/joncampbell123/dosbox-x/releases/download/dosbox-x-v2024.07.01/dosbox-x-macosx-arm64-20240702034526.zip), running on an M1 MacBook Pro.

**Use this at your own risk. It works for me, but If you should loose data or whatever don't blame me. Please refer to the LICENCE file.**

## Operation

*WordStar* documents must be in a particular directory (or one of its subdirectories). On my system I've set this to `~/Documents/WordStar`,
but you can set it to anywhere.

Double-clicking on one open it with *WordStar* within the *DOS* emulator.

Documents can also be opened from the command line. Use the command `wordstar -h` for help with that. Note that *WordStar* documents must still reside under the *WordStar* document directory.

## Installation

### Install *DOS-Box-X*

### Download or clone this repository

On my system it lives at `~/Applications/WordStar`, which I'll hereon refer to as just `WordStar`.

### Unpack the *WordStar* archive

Unpacking Robert J. Sawyer's *WordStar 7* archive will produce a folder named `WS`. Put it inside of `WordStar/DOS root/`.

### Install the fonts

Robert J. Sawyer's *WordStar 7* archive includes fonts for use with *DOS-Box-X*. They are mono-spaced `.ttf` fonts that include [code page 437](https://en.wikipedia.org/wiki/Code_page_437). Use the built-in *Font Book* to install any you want to use. The configuration in the repository uses *DejaVu Sans*.

### Delete the key-mapping file (probably)

On my system, I use *Karabiner-Elements* to remap my caps-lock key to act as the right control key, making the left control key redundant. Out of the box, DOS-Box-X uses F-12 as a modifier key, which it calls "host". In the file `WordStar/mapper-dosbox-x.map` I have redefined the left control key as this "host" key. If this won't work for your system configuration, delete the file—it's the only modification I've made to the default map.

There is another way to put move the control key to where the caps-lock is, using a *DOS* utillity located at `WordStar/DOS root/WS/SWAP.COM`. I have yet to try it.

### Customize the *BASH* script

#### Locations of things

The first section of the script `WordStar/wordstar` specifies the locations of things; most depend on where you've put your `WordStar` folder:

- `DOC_ROOT` specifies where *WordStar* documents will be kept. I've defined mine as `$HOME/Documents/WordStar`', but anywhere will do. Only files under this directory will be reachable by *WordStar*.
- `C_DRIVE` should point to `WordStar/DOS root`
- `CONFIG` should be ``WordStar/dosbox-x.conf`
- `DOSBOX_X`, if installed as an application, should be `/Applications/dosbox-x.app/Contents/MacOS/dosbox-x`. If you've installed *DOSBox-X* via *home brew* or something it will be somewhere else.

#### Fonts

If you've decided on using other fonts, you'll also need to change the following lines with your fonts' names:

```
	-set 'ttf font=dejavusansmono'
	-set 'ttf fontbold=dejavusansmono-bold'
	-set 'ttf fontital=dejavusansmono-oblique'
	-set 'ttf fontboit=dejavusansmono-boldoblique'
```

And to resize the font and window, change these lines:

```
	-set 'ttf ptsize=30'
	-set 'ttf lins=30'
	-set 'ttf cols=96'
```

I've picked values that work well with my screen, your mileage may vary.

Deleting these seven lines will use the values defined in the configuration file provided by Robert J. Sawyer's *WordStar 7* archive, which uses the Iosevka Fixed typeface family.

#### Put it on your `PATH`

If you want to conveniently run *WordStar* on the command line from anywhere, make a symbolic link to the `WordStar/wordstar` script somewhere on your path. (There are other ways to do this, with trade-offs.)

On my system I put a symbolic link at `~/.local/bin` with the command:

```bash
ln -is ~/Applications/WordStar/wordstar ~/.local/bin/
```

Again, YMMV—you might not even have a directory at that location.

### Make an application

If you want to open a `.WS` file with *WordStar* by default you'll need a default application. One can be made with the built-in app *Automator*.

1. Create a new document of the type 'Application'.
2. On the leftmost panel, select the Library called 'Utilities'
3. On the list to the right of that, double-click 'Run Shell Script'
4. For the "Shell", select "/bin/sh" , and for "Pass Input" select "to stdin".
5. In the textbox, enter `~/.local/bin/wordstar "$@"`, if that's where you put a symbolic link earlier. One could also replace that with `WordStar/wordstar`, wherever you happened to put that, but remember the `"$@"` at the end, that's how the filename of the document you want to open is passed along.
6. Save your application as "WordStar" or whatever, and optionally [change its icon](https://support.apple.com/en-ca/guide/mac-help/mchlp2313/10.13/mac/10.13). Some icon options are included in the folder `WordStar/icons`. 
7. Set your new application as the default application for `.WS` files. Instructions to do this can be found elsewhere.

Note that this will only work for `.WS` files located in the folder defined by `DOC_ROOT` in the *BASH* script.





---

This project includes the following resources, which may be subject to their own copyrights and licenses.

In the `icons` directory:

- the `.svg` file was derived from a _WordStar_ logotype, the code for which was found on [seeklogo.com](https://seeklogo.com/vector-logo/440979/wordstar).
- the `.png` files were converted from `.ico` files found in the `WS` folder of Robert J. Sawyer's WordStar 7 Archive.
