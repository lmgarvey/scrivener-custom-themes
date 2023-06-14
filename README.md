# scrivener-custom-themes
(Specifically for the Windows desktop app) I couldn't find an easy reference for what certain colors and sections were when trying to customize my layout, so I decided to make one!

Easiest way to customize your layout:
- `File -> Options -> Appearance`, go nuts! There are some things that cannot be modified like this, though - the main bar, that small left edge of the binder where the dropdown arrows are, that sort of thing.

More involved way to customize your layout:
- `Window -> Themes`
- There are some predefined themes, any of which you can use out of the box
- Alternatively, you could look up some themes to download and import. For example, included in this repo is a file called `solalight.scrtheme`. If you download this file, you can do `Window -> Themes -> Load Theme from File`, then select `solalight.scrtheme`. You could also select to *import* the .scrtheme file, which should put it into the Imported Themes folder
- Unfortunately, this won't be too exciting to look at - `solalight.scrtheme` is just the predefined 'Solarized Light' theme, but if you don't want to go to the trouble of grabbing one through Scrivener, you can instead just take it from here.

The hard way (what we're doing (don't worry, it's not that hard (because I'm doing the hard part for both of us))):
- To start, you'll need a .scrtheme file, since we mess with colors by modifying .qss and .pal files. These can be found a couple of ways: either download the .scrtheme file I have in this repo, or do `Window -> Themes -> Save Theme to File`. The latter of these will require you having selected a different theme than the default, but the former is pretty simple, anyway.
- To be able to modify those files, you'll want to change the file extension - eg, for my purposes, I would rename `solalight.scrtheme` to `solalight.zip`. This usually gives me a warning about changing the extension, but that's fine.
- Extract the files to wherever you'd like. There should be four in there:
  - solalight.pal   <-- This is your palette file. Naming colors in here allows you to call on them in the .qss file, eg `background-color: palette(some-color)`.
  - solalight.prefs   <-- This is for your personal preferences. For example, it includes the line `AutoCorrection\capitalizeI=false`, meaning that typing the letter 'i' by itself will not automatically capitalize it. We won't be touching this.
  - solalight.qss   <-- This is where you can get more specific than the palette file. The font bars at the top will by default be the same color as the tool tips, but if you want them to be different colors, you would change that sort of thing in here.
  - solalight.xml   <-- This is the basic .xml file, which tells Scrivener where to find all the information and customization you've done. We won't be touching this.
- Cool, we're ready to get started! Next, you'll want to boot up your favorite software for modifying .qss and .pal files (I'm using CLion because that's what they defaulted to, but any coding program should work. You could even use a Notepad if you wanted to).
- From there, you can go off and change the colors to your heart's content. `solalight.pal` is already commented with what things are (shoutout to the creators of the predefined themes for including those!), and I'm slowly working on adding similar comments to `solalight.qss`.
- Once you've changed everything as you wish (or when you want to check how things are looking), you'll take the four files and put them into a .scrtheme file. I've been doing this by selecting all four, compressing to a .zip file, then changing the file extension.
  - If you're on Windows, make sure all four items make it into the .scrtheme file. Simply right-clicking the folder and selecting `Compress to zip file` seems to skip over the .xml file, which will not work. Selecting all four files inside the folder and compressing them does the trick.
- When you have that .scrtheme file ready to go, just load it into Scrivener and restart the program to see your theme! See the 'More involved way to customize your layout' section above for a description on how to do this.


Now let's get into the weeds of the hard way. To start, here is the predefined 'Solarized Light' theme, as well as its color palette:

![main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/d773eb57-8b2c-4028-a28e-5bbfc0e038bd)

![palette](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/7c45713e-0bd0-4b40-ba58-d5272aa48184)

The names on the color palette match up to those found in `solalight.pal` - this is the color palette file, from which Scrivener will pull the desired colors and place them where they go. Conveniently for us, the palette file is commented with where you can expect the colors to show up.

![red main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/fb65b8e0-da92-48e2-894d-124e3d3bd1dc)

As seen above, there's some splashes of red now. That is because I went into `solalight.pal` and changed the value of the 'Base' color to be rgb(255,0,0). In this way, you can make broad changes across the entire interface.

If you check out the `solalight.qss` file, you will notice the following snippet:

`QToolTip {

    color: palette(text);
    
    background-color: palette(base);
    
    border: 1px solid palette(dark);
    
    border-radius: 4px;
    
}`

Tool tips are the little boxes that pop up when you hover over certain documents and icons, describing what they are or what they do. Shown above is a tool tip from hovering over 'The Basics' folder. Because QToolTip calls `palette(base)` when defining its background color, it uses that modified `Base(255,0,0)` that I changed in the palette file. If I go in and manually change that code to be:

`QToolTip {

    color: palette(text);
    
    background-color: rgba(0,255,0,130);
    
    border: 1px solid palette(dark);
    
    border-radius: 4px;
    
}`

we will now see a different color tool tip box:

![green main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/bc38eae4-8dd6-4fe5-aa40-76a9d15d8b5b)

Notice that while the tool tip box is now green, the other spots of red stayed. This is because, instead of changing the palette color, this time we directly changed one item (the tool tip). You might have also noticed that I used rgba, not rgb. This is because including the 'a' allows us to determine the opacity of the color, with 0 being transparent and 130 being opaque. Shown below is what it would look like if I had instead used `rgba(0,255,0,0)`.

![black main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/91744734-2bbb-44cd-9914-c66d6b3437b4)

In this way, you could poke around and figure out what colors map to where, but doing it one at a time, then zipping up the files, restarting Scrivener, and searching for where they popped up is tedious (just trust me on this one). You could also revamp the whole theme at once, instead of specifics, by just changing the color values in the `solalight.pal` file, as demonstrated above.

To save you the trouble, I'm going to try to define each of the entries in the `solalight.qss` file, so you know what changes where.

