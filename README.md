# _master_ branch
On Jan 24th we merged _godot-3.2_ branch into _master_. Currently using **Godot 3.2rc3**. Our next release will follow shortly after offical Godot 3.2 release.

### Changes
* Improved Planetarium GUI visibility control. GUI won't disapear when mouse in margin between GUI and screen edge.
* Full screen toggle (Shift-F) hides/shows all GUI for Planetarium. 
* Planetarium uses common MainMenu rather than its own menu. This allows add-ons or other external code to use MainMenu API to add buttons for Planetarium.
* Copyright notices updated for 2020.
* Fixed "Hide HUD when close" option to work without restart.

### Bug fixes
* Fixed bug causing target body to disappear momentarily during transition from Top to Zoom viewpoint (due to not updating `near` property during camera move).

### 3.2 compatibility fixes
* Fixed GUI widgets to work with 3.2 button signal changes. (Not compatible with Godot 3.1.2.)

# _godot-3.2_ branch (submodule only)
Moved changes above. This branch will be deleted shortly.
