# _master_ branch
Currently using **Godot 3.2**; some changes are not compatible with 3.1.2! Our next release will follow shortly after offical Godot 3.2 release.

### Changes
* Improved Planetarium GUI visibility control. GUI won't disapear when mouse in margin between GUI and screen edge.
* Full screen toggle (Shift-F) hides/shows all GUI for Planetarium. 
* Planetarium uses common MainMenu rather than its own menu. This allows add-ons or other external code to use MainMenu API to add buttons for Planetarium.
* Copyright notices updated for 2020.
* Fixed "Hide HUD when close" option to work without restart.
* Renamed ivoyager directories: "system_tree" & "system_refs" to "tree_nodes" & "tree_refs".
* Made tree processing more logical: TreeManager subscribes to Timekeeper, calls tree_manager_process() for VoyagerCamera and then Body instances.

### API breaking changes
* Removed VoyagerCamera "processed" signal.
* Changed signature & return value for SaverLoader.debug_log() function. This is a fix for the free-standing Procedural Saver/Loader 1.1 in the Godot Asset Library. 

### 3.2 compatibility fixes
* Fixed GUI widgets to work with 3.2 button signal changes. (Not compatible with Godot 3.1.2!)

### Bug fixes
* Fixed body momentary disappearance during camera move (due to not updating `near` property).
* Fixed giant sun when loading game that was fully zoomed out.
* Fixed date/time display when loading game that was paused.
