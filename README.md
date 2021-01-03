# _master_ branch
Godot version: **3.2.3**

Requires: **ivoyager_assets-2020-05-28**: [download here](https://github.com/ivoyager/changelogs/releases/download/dev-assets/ivoyager_assets-2020-05-28.zip)

## General Update
The project was on hiatus for much of the second half of 2020, but we are back for 2021! My near-term goal is to get v0.0.7 out in January. We are still in alpha so there are still breaking changes (probably some undocumented in the next version). I suspect that we will remain in "alpha" until Godot 4.0 release since that will create many more breaking changes. After 4.0, perhaps in mid-2021, when all is updated and working well again, we'll release our "beta" and then move on to official "1.0" release. Our API should be reasonably stable with the beta release.

## Added
* Latitude & longitude GUI.
* Camera can track orbit (as before) or track ground (**new!**) or neither (camera stays fixed in space relative to its parent object).

## Changes
* Translations are loaded from Global.translations so extensions can add w/out access to project.godot.
* Unicode escape using \uHHHH (where HHHH is a hexidecimal value) can now be used in data table files and localized text files. To make this work for localized text, text.csv files must be reimported with compress OFF. (This is a GDScript patch until Godot issue [#38716](https://github.com/godotengine/godot/issues/38716) gets fixed.)
* Changed .gitignore to allow tracking of export_presets.cfg in the project directories.
* HTML5 export projects close their own browser window on quitting.
* Improved Planetarium GUI response to window resizing.
* GUI "locks" moved to options area (lower-right) in Planetarium.
* Better sun "slice" image in the navigator panel.
* GUI widgets (ivoyager/gui_widgets/) are much improved in their modularity. They should be mostly drag-and-drop into new GUI scene trees (see example GUI in the Project Template).

## API-breaking changes
* Removed gui_planetarium from ivoyager submodule. The planetarium extension project now contains its own GUI.
* The Project Template now has its own GUI in directory replace_me/example_gui. (The directory ivoyager/gui_game is depreciated and will be removed!)

## Bug fixes
* Fixed visibility issues related to recent Godot versions.
* [Assets hotfix 0.0.6a] Resized images that weren't a power-of-2 size (throws errors in HTML5 builds).
* [Assets hotfix 0.0.6a] Fixed some import settings: flags/srgb ON for 3D assets, OFF for 2D; Mipmaps ON for everything (was off for 2D).
* Fixed stray node after opening Credits.
* Fixes for fullscreen toggle in Planetarium (HTML5 projects)
