# Current _master_ branch (v0.0.9-dev)
Under development using Godot 3.3 (just released!). Note: For asteroids to work in Godot 3.3 exports, you will need to remove .gdignore from ivoyager_assets/asteroid_binaries/. This will be fixed in a new assets release for v0.0.9.

Requires non-Git-tracked **ivoyager_assets-0.0.7**; find in [ivoyager releases](https://github.com/ivoyager/ivoyager/releases).

See cloning and downloading instructions [here](https://ivoyager.dev/download/).

March 31 development version (7bec948) is on our website! [Try it!](https://www.ivoyager.dev/planetarium/) We'll release v0.0.9-alpha soon after Godot 3.3 release.

## Project Changes
The first two will break external projects using the ivoyager submodule! Make changes as needed.
* [project breaking!] The Universe node was moved from the ivoyager submodule to the top level project directory. External projects can now add scenes to the simulator root node in the editor (before you could do this only by code).
* [project breaking!] [universe.gd](https://github.com/ivoyager/project_template/blob/master/universe.gd) now has the constants that define base SI units. By "externalizing" this, external projects can now change simulator internal representation of values (in particular, METER, which sets the scale of the simulation).
* We are no longer maintaining a "web-deployment" branch for the Planetarium. Instead, the master branch *is* the web deployment (e.g., it uses GLES2). Basically, our [Web Planetarium](https://www.ivoyager.dev/planetarium/) has become our main "product." You can still switch to GLES3 and export a functioning Windows app.
* Solar system data tables are now tab delineated .tsv files rather than .csv. The switch was needed for [this](https://github.com/godotengine/godot/issues/47061) Godot issue, but it's a good switch anyway. Tabs are easy to add within a cell using "\t", so we no longer need quote-enclosed cells to deal with our delineator.
* After years of frustration with Excel "interpreting" and modifying table values (e.g., changing the Sun's GM from 1.32712440018e20 to 1.33E+20) and trying to thwart that with preventative prefixes (but missing cases) I have switched to a new .csv/.tsv editor: [Ron's CSV Editor](https://www.ronsplace.eu/Products/RonsEditor/Download). So far, it's working superbly! The consequence, however, is that I'm no longer trying to maintain "Excel-safety" in our data tables, so .tsv files opened and saved in Excel will be ruined in many cases.

## Added
* New IOManager manages a separate thread for I/O including resource loading and other file reading/writing. All functions are called on the Main thread if external project sets Global.enable_threads = false.
* Many new "something_requested" signals in [Global](https://github.com/ivoyager/ivoyager/blob/master/singletons/global.gd). These can be used in lieu of direct calls to most functions in StateManager and SaveManager (and others).
* Expanded API in [Body](https://github.com/ivoyager/ivoyager/blob/master/tree_nodes/body.gd) and [Orbit](https://github.com/ivoyager/ivoyager/blob/master/tree_refs/orbit.gd) classes.
* Expanded data display for all astronomical bodies with closeable sections and subsections. (Content can be customized by external project.)
* Expanded wiki links for many data display labels and items (must be enabled, as is the case for the Planetarium).
* Added new Composition object. The new Body.components dictionary can hold any number of Composition instances representing anything. (I, Voyager uses for atmosphere chemical composition for display.)
* Added [data/solar_system/TABLES_README.txt](https://github.com/ivoyager/ivoyager/blob/master/data/solar_system/TABLES_README.txt) with info and rules for our data table system.
* Added capability for language localized Wikipedia links. All someone needs to do is add a table column "es.wikipedia", "de.wikipedia", etc., and add "es", "de", etc., to Global.wikipedia_locales.
* Added capability for an internal game wiki (a la Civilopedia). For this, add table column "wiki" and set Global.use_internal_wiki.

## Changes
* External project can set root node of the simulation by setting ProjectBuilder property "universe".
* Better feedback from save/load system for checking game-state consistency.
* "Program nodes" are now children of Universe rather than Global. All nodes with persist data are now under Universe, which helps with recent save/load changes.
* Non-HTML5 Planetarium now has a boot screen.
* Moved pale_blue_dot.png to project directory level. It's boot image for our projects, but now easier to remove for external project developers.
* Smoother progress bar progress during start and load. It's now linked to tasks completed by I/O thread.
* Body object reorganized with most properties moved to new "characteristics" dictionary (for non-object properties) or "components" dictionary (for objects).
* Improvements to SaveBuilder encoding of objects; SaveBuilder optimizations.
* Moved remaining init code from Global to several new initializer classes. This is better organization and allows extension projects to modify.

## API-breaking changes
* Class renamings:
    * QtyStrings -> QtyTxtConverter
    * ModelGeometry -> ModelController (maintains data related to body orientation in space)
    * SaverLoader -> SaveBuilder (also changed API substantially)
* Class split: new SaveManager has save/load related functions previously in StateManager.
* Removed class "Properties" (was subsequently renamed "BodyCharacteristics" before removal). Replaced by Body.characteristics dictionary.
* Many Body properties were moved into Body.characteristics dictionary.
* Function name changes in StateManager.
* Moved init related signals from ProjectBuilder to Global.
* Renamed Global signal "gui_refresh_requested" -> "update_gui_needed".
* Added leading underscore to ivoyager "virtual" functions: `_extension_init()` and `_project_init()`. (Note: subclasses can override, unlike Godot virtual functions.)
* Changes in TableReader "build_" function signatures; renamed "conv_" functions to "convert_".
* Renamed ProjectBuilder dictionaries to be more consistent with file system directories.
* Removed Global arrays "camera_info" and "mouse_target". Info from these are contained in new VisualsHelper class.

## Bug fixes
* Fixes to mouse_filter in various GUIs (was preventing selection of Iapetus).
* Fixed bug in SelectionData widget that allowed it to proliferate Labels on each game load without clearing.
* Fixed "?" display for moon masses.
* Fixed bug preventing "Top" view from showing whole system.
* Various get function errors in Body and Orbit were identified and fixed while expanding data display.
* Fixed lat/long display bugs.
* Fixed various problems related to retrograde orbit or rotation.
* Fixed some precision (significant digits) errors in data display.
* Fixed bug causing moons to flicker or disappear at high game speeds.
