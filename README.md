# v0.0.8 just released! (current _master_ branch)
Developed using **Godot 3.2.3** (tested & seems ok in 3.2.4-rc1)

Requires non-Git-tracked **ivoyager_assets-0.0.7**; find it in [ivoyager releases](https://github.com/ivoyager/ivoyager/releases).

See download instructions and links [here](https://ivoyager.dev/download/). 

**Repository changes!** I changed the names of the two "project" repositories, shortening to just "planetarium" and "project_template". The old URLs will continue to work so nothing should break. I deleated both the "issues" and "downloads" repositories (this was bad practice). Issues and downloads are now found in their respective project or submodule repositories, although the vast majority of issues will involve the submodule [here](https://github.com/ivoyager/ivoyager/issues).

## Added
* Network sync capability added in StateManager, Timekeeper and Body for multiplayer support. (Note: We won't have a NetworkLobby in core ivoyager, since that is very application-specific. But core will have signals and rpc calls to keep a network game synched on the solar system side.)
* Added [Scheduler](https://github.com/ivoyager/ivoyager/blob/master/prog_refs/scheduler.gd). This allows you to easily connect to interval signals based on simulator time (based on any or as many intervals as you need). I, Voyager uses this to update Orbit based on element rates (precessions, etc.).
* New MDFileLabel widget can read an .md file and convert (some) markdown codes to BBCode. It's narrowly coded now to read ivoyager/CREDITS.md for in-app display, but it could be improved to read more markdown codes.
* Added mouse-cursor-shape feedback (pointy finger, etc.) for main 3d screen selectables and some GUI elements.
* Hints for all GUI input controls.
* Added time setting functionality in Planetarium (using TimeSetPopup + TimeSetter widget in core ivoyager).

## Changes
* Updates to README.md, CREDITS.md, LICENCE.txt, and export_presets.cfg.
* Standardized useage of NAN to mean missing or not applicable (don't display) and INF to mean applicable but unknown (display as "?"). This affects return of TableReader functions for float values.
* TranslationImporter reports duplicate text keys.
* Improved 3d body mouse-click selection and screen drags. These functions now happen in ProjectionSurface (removed obsolete MouseClickSelector).

## API-breaking changes
* Debug is no longer a singleton node! It's now a static Reference class. This must be updated in your project.godot file, or Editor/settings/autoload, if you use ivoyager submodule in your own project! (Also removed Debug functions that probably weren't used by anyone.)
* Many enums renamed (for internal consistency)
* Class renames:
    * Registrar -> BodyRegistry
    * HUD2dSurface -> ProjectionSurface
* Overhauled Timekeeper API to more correctly use Julian Day Number, Julian Day, UT, etc.
* ContainerSized, ContainerDraggable & ContainerDynamic generalized to modify Control parent and renamed ControlSized, ControlDraggable & ControlDynamic

## Bug fixes
* Fixed bug preventing hotkey action removal (when not replaced)
