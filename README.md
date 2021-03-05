# current _master_ branch (v0.0.9-dev)
Developed using **Godot 3.2.3** (ok in 3.2.4-rc1; there is a lighting problem in -rc2 that has been reported and fixed, so waiting to test -rc3)

Requires non-Git-tracked **ivoyager_assets-0.0.7**; find it in [ivoyager releases](https://github.com/ivoyager/ivoyager/releases).

See cloning and downloading instructions [here](https://ivoyager.dev/download/). 

## Project Changes
These will break external projects using the ivoyager submodule! Make changes as needed.
* The Universe node was moved from the ivoyager submodule to the top level project directory. External projects can now add scenes to the simulator root node in the editor (before you could do this only by code).
* [universe.gd](https://github.com/ivoyager/project_template/blob/master/universe.gd) now has the constants that define base SI units. By "externalizing" this, external projects can now change simulator internal representation of values. In particular, constant METER determimes the scale of the simulation.

## Added
* New IOManager manages a separate thread for I/O including resource loading and other file reading/writing. All functions work on the Main thread if external project sets Global.enable_threads = false. Unfortunately, we won't be able to use threads for the Web Planetarium until Godot 4.0. (Note: progress bar does not progress in most cases if enable_threads = false. I removed it in the Web Planetarium.)
* Many new "something_requested" signals in Global. These can be used in lieu of direct calls to most functions in StateManager and SaveManager (and others). 

## Changes
* Universe is now replaceable in ProjectBuilder.
* Better feedback from save/load system for checking game-state consistency.
* "Program nodes" are now children of Universe rather than Global. All nodes with persist data are now under Universe, which helps with recent save/load changes.
* Non-HTML5 Planetarium now has a boot screen.
* Moved pale_blue_dot.png to project directory level. It's boot image for our projects, but now easier to remove for external project developers.
* Much smoother progress bar progress during start and load. It's now linked to tasks completed by I/O thread.

## API-breaking changes
* Save/load related functions moved from StateManager to new SaveManager.
* Function name changes in StateManager.
* Renamed SaverLoader -> SaveBuilder, and changed API substantially.
* Moved init related signals from ProjectBuilder to Global.
* Renamed Global signal "gui_refresh_requested" -> "update_gui_needed".
* Added leading underscore to ivoyager "virtual" functions: `_extension_init()` and `_project_init()`.

## Bug fixes
* Fixes to mouse_filter in various GUIs (was preventing selection of Iapetus).
* Fixed bug in SelectionData widget that allowed it to proliferate Labels on each game load without clearing.
* Fixed "?" display for moon masses.
