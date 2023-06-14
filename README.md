# scrivener-custom-themes
(Specifically for the Windows desktop app) I couldn't find an easy reference for what certain colors and sections were when trying to customize my layout, so I decided to make one!

Easiest way to customize your layout:
- `Window -> Themes`
- There are some predefined themes, any of which you can use out of the box
- Alternatively, you could look up some themes to download and import. For example, included in this repo is a file called `testing.scrtheme`. If you download this file, you can do `Window -> Themes -> Load Theme from File`, then select `testing.scrtheme`. You could also select to *import* the .scrtheme file, which should put it into the Imported Themes folder
- Naturally, `testing.scrtheme` isn't intended to look pretty - it's intended to illustrate where certain colors are. Searching things like `scrivener custom pastel theme` or `scrivener custom solarized theme` will bring up other themes you could use instead.

More personal way to customize your layout: `File -> Options -> Appearance`, go nuts! There are some things that cannot be modified like this, though - the main bar, that small left edge of the binder where the dropdown arrows are, that sort of thing.

The hard way (what we're doing (don't worry, it's not that hard (because I'm doing the hard part for both of us))):
- To start, you'll need a .scrtheme file, since we mess with colors by modifying .qss and .pal files. These can be found a couple of ways: either download the .scrtheme file I have in this repo, or do `Window -> Themes -> Save Theme to File`. The latter of these might require you having selected a different theme than the default, but the former is pretty simple, anyway.
- To be able to modify those files, you'll want to change the file extension - eg, for my purposes, I would rename `testing.scrtheme` to `testing.zip`. This usually gives me a warning about changing the extension, but that's fine.
- Extract the files to wherever you'd like. There should be four in there:
  - testing.pal   <-- This is your palette file. Naming colors in here allows you to call on them in the .qss file, eg `background-color: palette(some-color)`.
  - testing.prefs   <-- This is for your personal preferences. For example, it includes the line `AutoCorrection\capitalizeI=false`, meaning that typing the letter 'i' by itself will not automatically capitalize it.
  - testing.qss   <-- This is where you can get more specific than the palette file. The main menu bar will by default be the same color as that left edge of the binder, but if you want them to be different colors, you would change that sort of thing in here.
  - testing.xml   <-- This is the basic .xml file, which tells Scrivener where to find all the information and customization you've done. We won't be touching this.
- Cool, we're ready to get started! Next, you'll want to boot up your favorite software for modifying .qss and .pal files (I'm using CLion because that's what they defaulted to, but any coding program should probably work. You could even use a Notepad if you wanted to).
- To start, let's look at the eyesore that is the `New Project` window, using the testing.scrtheme theme:

![new project window](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/ef427a71-9d07-4879-b424-9a5b140aa31a)




