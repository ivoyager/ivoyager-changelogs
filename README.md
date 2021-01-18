# _master_ branch
Godot version: **3.2.3**

Requires: **ivoyager_assets-2020-05-28**: [download here](https://github.com/ivoyager/changelogs/releases/download/dev-assets/ivoyager_assets-2020-05-28.zip)

## General Update
The project was on hiatus for much of the second half of 2020, but we are back for 2021! My near-term goal is to get v0.0.7 out in January. We are in alpha so we still have many API breaking changes. I suspect that we will remain in "alpha" until Godot 4.0 release since that will create many more breaking changes. After 4.0, perhaps in mid- to late 2021, we'll release our "beta" and then move on to official "1.0" release. Our API should be reasonably stable with the beta release.

## Added
* Latitude & longitude GUI.
* Camera can track orbit (as before) or track ground (**new!**) or neither (camera stays fixed in space relative to its parent object).
* Above the gui_widgets directory there is a new directory called gui_mods. This directory includes drag-and-drop components that modify GUI operation:
   * ContainerSizedBySettings - This is added to the two PanelContainers in the GameExampleGUI and makes these resize when user changes GUI Size in Options.
   * ContainerDynamic - Replaces above to make PanelContainers draggable and resizable (w/ resizing margins) by the user. Used in Planetarium.
   * PanelVisOnMouseOverCkbx - Makes panel visible only when mouse is over or near it. A checkbox allows the user to lock it in visible state. Used in Planetarium.
   * ProjectCyclablePanels - Allows a key to cycle-through panels, making them visible (if hidden due to mod above) and grabbing focus.
* Added hint tooltips on mouse-over for most buttons, checkboxes, etc.

## Changes
* **Huge improvements to GUI modularity!** I, Voyager GUI widgets can be easily dropped into custom GUI scene trees. Widgets include dynamic labels and textures (e.g., CameraRange, DateTimeLabel, SelectionImage) and user controls (e.g., SpeedButtons, ViewButtons, SystemNavigator) that plug into I, Voyager core systems.
* Totally overhauled GUI for both the game template example (ivoyager/gui_example/example_game_gui.tcsn) and the Planetarium (planetarium/gui/pl_gui.tscn in the Planetarium repository) using the new modular widgets and mods.
* Translations are loaded from Global.translations so extensions can add w/out access to project.godot.
* Unicode escape using \uHHHH (where HHHH is a hexidecimal value) can now be used in data table files and localized text files. To make this work for localized text, text.csv files must be reimported with compress OFF. (This is a GDScript patch until Godot issue [#38716](https://github.com/godotengine/godot/issues/38716) gets fixed.)
* Changed .gitignore to allow tracking of export_presets.cfg in the project directories.
* HTML5 export projects close their own browser window on quitting.
* Better sun "slice" image in the navigator panel.

## API-breaking changes
* Many class renamings.
* Many existing GUI widgets were depreciated in favor of new, more modular widgets.
* Game template example GUI is now in directory ivoyager/gui_example/.
* Removed gui_planetarium directory from ivoyager submodule. The planetarium extension project now contains its own GUI.

## Bug fixes
* Fixed visibility issues related to recent Godot versions.
* [Assets hotfix 0.0.6a] Resized images that weren't a power-of-2 size (throws errors in HTML5 builds).
* [Assets hotfix 0.0.6a] Fixed some import settings: flags/srgb ON for 3D assets, OFF for 2D; Mipmaps ON for everything (was off for 2D).
* Fixed stray node after opening Credits.
* Fixes for fullscreen toggle in Planetarium (HTML5 projects)
