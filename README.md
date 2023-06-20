# scrivener-custom-themes
(Specifically for the Windows desktop app) I couldn't find an easy reference for what certain colors and sections were when trying to customize my layout, so I decided to make one!

[TK] at the beginning of a line means that section is incomplete, and I want to be able to find it later on.

Easiest way to customize your layout:
- `File -> Options -> Appearance`, go nuts! There are some things that cannot be modified like this, though - the main bar, that small left edge of the binder where the dropdown arrows are, that sort of thing.

More involved way to customize your layout:
- `Window -> Themes`
- There are some predefined themes, any of which you can use out of the box
- Alternatively, you could look up some themes to download and import. For example, included in this repo is a file called `solalight.scrtheme`. If you download this file, you can do `Window -> Themes -> Load Theme from File`, then select `solalight.scrtheme`. You could also select to *import* the .scrtheme file, which should put it into the Imported Themes folder
- Unfortunately, this won't be too exciting to look at - `solalight.scrtheme` is just the predefined 'Solarized Light' theme, but if you don't want to go to the trouble of grabbing one through Scrivener, you can instead just take it from here.

The hard way (what we're doing (don't worry, it's not that hard (because I'm doing the hard part for both of us))):
- To start, you'll need a .scrtheme file, since we mess with colors by modifying .qss and .pal files. These can be found a couple of ways: either download the .scrtheme file I have in this repo, or do `Window -> Themes -> Save Theme to File`. The latter of these will require you having selected a different theme than the default, but the former is pretty simple, anyway.
- To be able to modify those files, you'll want to change the file extension - eg, for my purposes, I would rename `solalight.scrtheme` to `solalight.zip` (though I've included both in this repo for you). This usually gives me a warning about changing the extension, but that's fine.
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

```
QToolTip {

    color: palette(text);
    
    background-color: palette(base);
    
    border: 1px solid palette(dark);
    
    border-radius: 4px;
    
}
```

Tool tips are the little boxes that pop up when you hover over certain documents and icons, describing what they are or what they do. Shown above is a tool tip from hovering over 'The Basics' folder. Because QToolTip calls `palette(base)` when defining its background color, it uses that modified `Base(255,0,0)` that I changed in the palette file. If I go in and manually change that code to be:

```
QToolTip {

    color: palette(text);
    
    background-color: rgba(0,255,0,130);
    
    border: 1px solid palette(dark);
    
    border-radius: 4px;
    
}
```

we will now see a different color tool tip box:

![green main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/bc38eae4-8dd6-4fe5-aa40-76a9d15d8b5b)

Notice that while the tool tip box is now green, the other spots of red stayed. This is because, instead of changing the palette color, this time we directly changed one item (the tool tip). You might have also noticed that I used rgba, not rgb. This is because including the 'a' allows us to determine the opacity of the color, with 0 being transparent and 130 being opaque. Shown below is what it would look like if I had instead used `rgba(0,255,0,0)`.

![black main](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/91744734-2bbb-44cd-9914-c66d6b3437b4)

In this way, you could poke around and figure out what colors map to where, but doing it one at a time, then zipping up the files, restarting Scrivener, and searching for where they popped up is tedious (just trust me on this one). You could also revamp the whole theme at once, instead of specifics, by just changing the color values in the `solalight.pal` file, as demonstrated above.

To save you the trouble, I'm going to try to define each of the entries in the `solalight.qss` file, so you know what changes where. This will be done by returning `solalight.pal` and `solalight.qss` to their initial states, as shown first and as included in this repo. Then I'll go through `solalight.qss` and make one item at a time be very bright colors, paired with a screenshot of where the item/color can be found. Ready? Let's-a go!

```
QToolTip {

    color: palette(text);

    background-color: palette(base);
    
    border: 1px solid palette(dark);
    
    border-radius: 4px;

}
```

We saw this before - tool tips appear when you hover over something with your mouse. 'color' is the color of the text in the box, 'background-color' is the color of the whole box, and 'border' is the color running along the edge of the box.

```
QStatusBar {
    
    background-color: palette(alternate-base);
    
    color: palette(mid);

}
```

[TK] Supposedly, this should be the bar along the very bottom, where you can see a document's word count, set word or character count targets, and set the status of a document or project. I cannot seem to change it, so we're moving on. (my guess is it comes from something to do with the .prefs file)

![green menu bar border](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/ba6d85f1-462f-479e-be10-09f53222f29c)

```
QMenuBar {
    
    background-color: rgba(255,0,0,130);
    
    border-bottom: 2px solid rgba(0,255,0,130);

}
```

The menu bar is that section along the top, with options like 'File', 'Edit', and 'Window', as well as the blank space between and past them. You can see here the bright green line running along the bottom of it - this is your `border-bottom`. [TK] The bar itself isn't red, which I again will assume is the fault of the .prefs file.

![red menu bar items](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/a795b47e-fda8-4e34-916a-cfb59168318b)

```
QMenuBar::item {
    
    spacing: 2px;
    
    padding: 3px 4px;
    
    background: rgba(255,0,0,130);

}
```

Menu bar items are the clickable options, eg 'File' and 'Edit.' In the included .qss file, background is set to 'transparent,' meaning that the items will match the color of the menu bar as set above. If you wanted them to stand out and be a different color, you would do it here.

![menu bar item hovered](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/39c06088-b782-4951-a01c-a29fb3da5be8)

```
QMenuBar::item:selected {
    
    background-color: rgba(255,0,0,130);
    
    border-left: 1px solid rgba(0,255,0,130);
    
    border-right: 1px solid rgba(0,0,255,130);

}
```

A 'selected' menu bar item just means that your mouse is hovering over it, without clicking the option. Shown here, I am hovering over the 'Help' option. If you look closely, you can also see that the left and right borders are different colors, too.

![menu bar item clicked](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/1a920add-986f-4f23-9377-79a0aa21ab9c)

```
QMenuBar::item:pressed {
    
    background-color: rgba(255,0,0,130);
    
    border-left: 1px solid rgba(0,255,0,130);
    
    border-right: 1px solid rgba(0,0,255,130);

}
```

A 'pressed' menu bar item is one that has been clicked, revealing its dropdown menu. Here, I've clicked the 'Help' option, and you can again see that the borders are different colors, too.

![menu dropdown](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/4fe42548-9981-498d-b84d-4b446c02ca5b)
![menu dropdown thick border](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/3c0a4868-be46-4b84-bdbf-70bec7693a4d)

```
QMenu {
    
    background-color: rgba(255,0,0,130);
    
    border: 1px solid rgba(0,255,0,130);

}
```

A plain old 'Menu' is the dropdown that appears when you click an option. Here again, I've clicked the 'Help' option. The main color is red, and the edges are green. Just for fun, I've also included what it looks like if I change the border from 1px to 10px.

![menu items](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/73f089e4-fea2-462c-bc1e-db4efbdba683)

```
QMenu::item {
    
    min-width: 120px !important;
    
    background: rgba(255,255,255,130);
    
    border: 1px solid rgb(255,0,0,130);
    
    padding: 1px 20px 1px 26px !important;
    
    margin: 1px !important;

}

QMenu::item:disabled {
    
    color: rgba(0,255,0,130);

}

QMenu::item:selected {
    
    border-color: rgba(0,0,255,130);
    
    background: rgba(0,255,255,130);

}
```

There's a bit more going on here. I've selected the 'Documents' tab. Each option within the dropdown is called an item. Unhovered and left alone, you can see they are all white (rgba(255,255,255,130)) with red borders (rgba(255,0,0,130)). The ones with green text (rgba(0,255,0,130)) are 'disabled' items, meaning they cannot be clicked on for some reason or another. Finally, I have my mouse hovering over the 'Snapshots' item, highlighting it cyan (rgba(0,255,255,130)) and giving it a blue border (rgba(0,0,255,130)).

![menu icon checked](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/e78e57dc-d202-45ec-9f42-dbf4d97645db)

```
QMenu::icon:checked {
    
    background-color: rgba(255,0,0,130);
    
    background: rgba(0,0,255,130);
    
    border: 1px solid rgba(0,255,0,130);
    
    border-radius: 2px;

}
```

Here, I've selected the 'Format' tab and the 'Paragraph' item. Since the paragraph currently being modified is aligned left, that's the option that is checked, by being highlighted blue (rgba(0,0,255,130)) and outline in green (rgba(0,255,0,130)). The base .qss file actually uses `background-color` and not `background`, which didn't seem to change anything, hence why I added the `background` line above. If `background-color` were used and appeared somewhere, it would be red (rgba(255,0,0,130)).

![right arrow](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/edf26110-d4e1-471c-9590-b863f881ccca)

```
QMenu::right-arrow {
    
    width: 10px;
    
    height: 10px;
    
    margin-right: 1px;
    
    background: rgba(0,0,255,130);
    
    border: 1px solid rgba(0,255,255,130);

}
```

In the previous screenshots, you could see that the right arrows, such as in the `Format -> Paragraph` item, were little greater-than signs. By adding the background and border fields (which are not in the base .qss file), I've changed them to blue boxes outlined in cyan. [TK] I think you could also make this an image, if you want.

![menu separator and indicator](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/121f734d-4f14-4c2d-9cad-6ae8c7debe33)

```
QMenu::separator {
    
    height: 1px;
    
    background: rgba(255,0,0,130);
    
    margin-left: 10px;
    
    margin-right: 10px;

}

QMenu::indicator {
    
    position: absolute!important;
    
    background-color: rgba(0,0,255,130);
    
    top: 2px!important;
    
    left: 2px!important;
    
    width: 13px!important;
    
    height: 13px!important;

}
```

The red lines are the separators, and the blue boxes are the indicators (checkboxes of whether something is or is not selected).

[TK] There are a bunch of images for indicators, which should probably be customizable, but I'm not certain at the moment where the resources folder is to *put* those images, so I'm going to skip that section for now.

![main window separator](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/fe96f12e-3313-4f7b-84df-a6a3d29225a9)

```
QMainWindow::separator {
    
    width: 6px;
    
    height: 5px;
    
    padding: 2px;

}

QMainWindow::separator:hover,

QSplitter::handle:hover {
    
    background: rgba(0,255,255,130);

}
```

If you look at the right edge of the binder scrollbar, you will see a cyan line running along it (rgba(0,255,255,130)). This is the bar that appears when you hover over that edge to click and drag, for resizing the binder. The same color would appear at the left edge of the inspector, and if you have two documents open at once in split view, you will also find a cyan line when resizing those. [TK] I have no idea what the main window separator is.

[TK] idk where this should go wrt the rest of the qss file so i'm putting it here. You can also change the icons directly in Scrivener, such as the little blue folder beside the 'Get Oriented' folder. [This](https://www.jenterpstra.com/blog/custom-scrivener-binder-icons-tutorial) page goes more in-depth, but the basic idea is to right-click the icon you wish to change, select 'Change Icon', and then either select an icon from text, or import an icon image you wish to use. The former would ideally use single characters, or else very short phrases if your screen allows for that. The latter is the more customizable version. I downloaded a 100x100 png of a fox and, using the latter method to select the image, used it to change the [icon](https://www.vexels.com/png-svg/preview/151733/cute-fox-cartoon-design) of my 'Get Oriented' folder:

![main page with a fox icon](https://github.com/lmgarvey/scrivener-custom-themes/assets/94126547/90d5f440-7b96-45db-9030-f3dce1e7a360)


As you can see, I now have a cute little fox instead of that blue folder icon. I added it using 'Manage Icons...', then selected it from the dropdown list of possible icons. [TK] There might be a more direct way to do this in the qss or prefs folder, where replacing 'Generic blue folder' with 'cute little fox' in one spot will make that fox appear as the relevant icon across all folders in the project with this theme, but i haven't found it (nor have i looked, tbh).
