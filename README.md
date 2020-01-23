# _master_ branch
Currently Godot version **3.1.2** but anticipating 3.2

### Changes
* Improved Planetarium GUI visibility control. GUI won't disapear when mouse in margin between GUI and screen edge.
* Full screen toggle (Shift-F) hides/shows all GUI for Planetarium. 
* Planetarium uses common MainMenu rather than its own menu. This allows add-ons or other external code to use MainMenu API to add buttons for Planetarium.
* Copyright notices updated for 2020.

### Bug fixes
* Fixed bug causing target body to disappear momentarily during transition from Top to Zoom viewpoint.

# _godot-3.2_ branch (submodule only)
Tested w/ Godot 3.2 release candidate 2. Will merge into _master_ with Godot 3.2 release.

### 3.2 compatibility fixes
* Fixed GUI widgets to work with 3.2 button signal changes. (Not compatible with Godot 3.1.2.)

### Changes
* Fixed "Hide HUD when close" option to work without restart.
