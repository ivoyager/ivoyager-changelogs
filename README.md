# master (after v0.0.2)
(Now using Godot **3.1.2.**)

### Added
* New GUI widgets. The idea here is to make existing "functional elements" (e.g., a set of related buttons) into self-contained scene widgets for easy use in project-specific GUI. This will be done on an as-needed basis.
   * SystemNavigator - NavigationPanel widget with the selectable sun/planets/moons.
   * ViewpointBox - SelectionPanel widget with Zoom/45/Top buttons.
   * FocalLengthBox - SelectionPanel widget with focal-length label & buttons.
   * CameraLock - NavigationPanel widget that locks/unlocks camera to main UI selection.
* Added project setting Global.asteroid_mag_cutoff_override. This can overide mag_cutoff for all groups normally set in data/solar_system/asteroid_group_data.csv. With the default mag_cutoff=15, we have 64,738 total asteroids. If you set the override to 100.0, you'll see all 647,000 asteroids. If you set the override to a value < 15.0, you'll have fewer than 64,738 asteroids. (Magnitude is smaller for larger objects!)

### Changes
* Widget RangeLabel sets its own visibility.
* Renamed "COPYRIGHT.txt" to "3RD_PARTY.txt" in all repositories. "COPYRIGHT" was interfering with GitHub recognition our Apache 2.0 license in LICENSE.txt. Also, "3RD_PARTY" is a better description of the contents.
* Many Controls such as MainMenu, MainProgBar and others are now safely removable.
* Widget fixes so they can be added before solar system build.
* Renamed "HUD2dControl" to "HUD2dSurface" and moved from wrong directory to gui_admin.
* Widget DateTime displays date/time text in red when time runs in reverse.

### API-breaking changes
* Renamed VoyagerCamera enum "VIEWPOINT_BUMPED_POINTING" to "VIEWPOINT_BUMPED".
* Renamed widget "CameraRange" to "RangeLabel".
* Moved some public vars from Main to Global (ivoyager_version, project_version, is_modded).

### Bug fixes
* Fixed var shadowing error.
* Fixed asteroid visibility save/load persistence.
* Fixed error in AsteroidGroup.max_apoapsis calculation.
