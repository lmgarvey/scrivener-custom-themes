# scrivener-custom-themes
(Specifically for the Windows desktop app) I couldn't find an easy reference for what certain colors and sections were when trying to customize my layout, so I decided to make one!

Fair word of warning, this is a work in progress, and there are some things I've yet to figure out. Those will be labeled [TK], so I can search for them as I come across new information.

Easiest way to customize your layout:
- `File -> Options -> Appearance`, go nuts! There are some things that cannot be modified like this, though - the main bar, that small left edge of the binder where the dropdown arrows are, that sort of thing.

More involved way to customize your layout:
- `Window -> Themes`
- There are some predefined themes, any of which you can use out of the box
- Alternatively, you could look up some themes to download and import. For example, included in this repo is a file called `testing.scrtheme`. If you download this file, you can do `Window -> Themes -> Load Theme from File`, then select `testing.scrtheme`. You could also select to *import* the .scrtheme file, which should put it into the Imported Themes folder
- Naturally, `testing.scrtheme` isn't intended to look pretty - it's intended to illustrate where certain colors are. Searching things like `scrivener custom pastel theme` or `scrivener custom solarized theme` will bring up other themes you could use instead.

The hard way (what we're doing (don't worry, it's not that hard (because I'm doing the hard part for both of us))):
- To start, you'll need a .scrtheme file, since we mess with colors by modifying .qss and .pal files. These can be found a couple of ways: either download the .scrtheme file I have in this repo, or do `Window -> Themes -> Save Theme to File`. The latter of these might require you having selected a different theme than the default, but the former is pretty simple, anyway.
- To be able to modify those files, you'll want to change the file extension - eg, for my purposes, I would rename `testing.scrtheme` to `testing.zip`. This usually gives me a warning about changing the extension, but that's fine.
- Extract the files to wherever you'd like. There should be four in there:
  - testing.pal   <-- This is your palette file. Naming colors in here allows you to call on them in the .qss file, eg `background-color: palette(some-color)`.
  - testing.prefs   <-- This is for your personal preferences. For example, it includes the line `AutoCorrection\capitalizeI=false`, meaning that typing the letter 'i' by itself will not automatically capitalize it.
  - testing.qss   <-- This is where you can get more specific than the palette file. The main menu bar will by default be the same color as that left edge of the binder, but if you want them to be different colors, you would change that sort of thing in here.
  - testing.xml   <-- This is the basic .xml file, which tells Scrivener where to find all the information and customization you've done. We won't be touching this.
- Cool, we're ready to get started! Next, you'll want to boot up your favorite software for modifying .qss and .pal files (I'm using CLion because that's what they defaulted to, but any coding program should probably work. You could even use a Notepad if you wanted to).
- From there, you can go off and change the colors to your heart's content. `testing.pal` is already commented with what things are (shoutout to the creators of the predefined themes for including those!), and I'm slowly working on adding similar comments to `testing.qss`.

For a more in-depth look at which things are where, I'm going to start with `testing.pal`. If you wanted, you could skip this and directly modify colors in `testing.qss`, but that would lead to a similar issue as mentioned above, where certain things (which live in `testing.prefs`) wouldn't be modifiable.
- To start, let's look at the eyesores that are the main window and the 'New Project' window, using the testing.scrtheme theme:

![main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/255f800c-0a66-423b-934e-de983c63780a)

![new project window](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/083bec0e-c9b9-41cb-b430-17ec9e8a8caf)

Things to note here:
- When describing a color in `testing.pal`, it will be in the format `ColorName(R,G,B)`
  - As mentioned before, it could be more direct to simply modify `testing.qss`, but this should hopefully give an idea of where certain things from the palette file show up
- The bright red behind 'Key Concepts' and on the left edge of the binder is found in `testing.pal` by the name `Base(255,0,0)`
- The light red making up the menu bar, the bottom bar, and the edges of the workspace is found in `testing.pal` by the name `Window(255,122,122)`
- The light orange of the scroll bar and the buttons is found in `testing.pal` by the name `ToolTipBase(255,129,18)`
- The medium orange behind the scroll bar is found in `testing.pal` by the name `Button(255,129,18)`
- [TK] I *think* the highlighted area around 'Getting Started' is found in `testing.pal` by the name `Button(255,129,18)`, but at a lower opacity. Not certain, though!
- [TK] Similarly, I *think* the highlighted area around 'Interactive Tutorial' is found in `testing.pal` by the name `Highlight(207,96,0)`, but at a lower opacity.
- The light yellow text of the menu options like 'File' and 'Edit', as well as the button titles like 'Options' and 'Open', are found in `testing.pal` by the name `WindowText(255,246,163)`
- The medium yellow text, such as that of 'Fiction' and 'Scriptwriting', is found in `testing.pal` by the name `Text(255,232,20)`
- The bright green text, such as that of 'Getting Started' on the 'New Project' window and the 'Help' menu option in the main window, are found in `testing.pal` by the name `ButtonText(209,255,153)`
- The purple highlight over the 'Help' menu option is found in `testing.pal` by the name `Midlight(184,71,245)`


