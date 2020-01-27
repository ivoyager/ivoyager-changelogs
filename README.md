# _master_ branch
On Jan 24th we merged _godot-3.2_ branch into _master_. We are currently using **Godot 3.2rc3**; some changes are not compatible with 3.1.2! Our next release will follow shortly after offical Godot 3.2 release.

### Changes
* Improved Planetarium GUI visibility control. GUI won't disapear when mouse in margin between GUI and screen edge.
* Full screen toggle (Shift-F) hides/shows all GUI for Planetarium. 
* Planetarium uses common MainMenu rather than its own menu. This allows add-ons or other external code to use MainMenu API to add buttons for Planetarium.
* Copyright notices updated for 2020.
* Fixed "Hide HUD when close" option to work without restart.
* Renamed ivoyager directories: "system_tree" & "system_refs" to "tree_nodes" & "tree_refs"
* Made tree processing more logical: TreeManager subscribes to Timekeeper, calls tree_manager_process() for VoyagerCamera and then Body instances.

### API breaking changes
* Removed VoyagerCamera "processed" signal

### 3.2 compatibility fixes
* Fixed GUI widgets to work with 3.2 button signal changes. (Not compatible with Godot 3.1.2!)

### Bug fixes
* Fixed bug causing target body to disappear momentarily during transition from Top to Zoom viewpoint (due to not updating `near` property during camera move).
* Fixed giant sun when loading game that was fully zoomed out
* Fixed date/time display when loading game that was paused
