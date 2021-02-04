# Current _master_ branch (v0.0.8-dev)
Under development using Godot **3.2.3** (not yet tested in 3.2.4 betas)

Requires: **ivoyager_assets-0.0.7**: [download here](https://github.com/ivoyager/downloads/releases/tag/v0.0.7-alpha)

Not much here yet! See recent changes in v0.0.7.md above.

**Repository name changes!** I changed the names of two repositories, shortening to just "planetarium" and "project_template". The old URLs will continue to work so nothing should break. But you might want to update your fork and local repository names (and Git remotes) for consistency. 

## Added
* Network sync capability added in StateManager, Timekeeper and Body for multiplayer support. (Note: We won't have a NetworkLobby in core ivoyager, since that is very application-specific. But core will have signals and rpc calls to keep a network game synched on the solar system side.)
* Added [Scheduler](https://github.com/ivoyager/ivoyager/blob/master/prog_refs/scheduler.gd). This allows you to generate and connect to interval signals based on simulator time. I, Voyager uses this to update Orbit based on element rates (precessions, etc.).
* New MDFileLabel widget can read an .md file and convert (some) markdown codes to BBCode. It's narrowly coded now to read ivoyager/CREDITS.md for in-app display, but it could be improved to read more markdown codes.

## Changes
* Updates to README.md, CREDITS.md, LICENCE.txt, and export_presets.cfg.

## API-breaking changes
* Many enums were renamed (for internal consistency)
* Class renames:
    * Registrar -> BodyRegistry

## Bug fixes
