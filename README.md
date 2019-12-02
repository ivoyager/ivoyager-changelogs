# master (after v0.0.2)
(Now using Godot **3.1.2.**)

### Added
* New GUI widgets. The idea here is to make most or all GUI "functional elements" (e.g., a set of related buttons) into self-contained scene widgets for easy use in project-specific GUI. This will be done on an as-needed basis.
   * SystemNavigator - this is the part of NavigationPanel with the selectable sun/planets/moons.
   * ViewpointBox - SelectionPanel widget with zoom/45/top
   * FOVBox - SelectionPanel widget for changing focal length

### Changes
* Widget RangeLabel sets its own visibility

### API-breaking changes
* VoyagerCamera enum "VIEWPOINT_BUMPED_POINTING" -> "VIEWPOINT_BUMPED"
* Renamed widget "CameraRange" -> "RangeLabel"

### Bug fixes
* Fixed var shadowing error
