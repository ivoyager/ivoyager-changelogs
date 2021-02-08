# Current _master_ branch (v0.0.8-dev)
Under development using Godot **3.2.3** (not yet tested in 3.2.4 betas)

Requires: **ivoyager_assets-0.0.7**: [download here](https://github.com/ivoyager/downloads/releases/tag/v0.0.7-alpha)

See other recent changes in v0.0.7.md above!

**Repository name changes!** I changed the names of two repositories, shortening to just "planetarium" and "project_template". The old URLs will continue to work so nothing should break. But you might want to update your fork and local repository names (and Git remotes) for consistency. 

## Added
* Network sync capability added in StateManager, Timekeeper and Body for multiplayer support. (Note: We won't have a NetworkLobby in core ivoyager, since that is very application-specific. But core will have signals and rpc calls to keep a network game synched on the solar system side.)
* Added [Scheduler](https://github.com/ivoyager/ivoyager/blob/master/prog_refs/scheduler.gd). This allows you to generate and connect to interval signals based on simulator time. I, Voyager uses this to update Orbit based on element rates (precessions, etc.).
* New MDFileLabel widget can read an .md file and convert (some) markdown codes to BBCode. It's narrowly coded now to read ivoyager/CREDITS.md for in-app display, but it could be improved to read more markdown codes.
* Added mouse-cursor-shape feedback (pointy finger, etc.) for main 3d screen selectables and some GUI elements.
* Hints for all GUI input controls.

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

## Bug fixes
