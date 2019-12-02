# master (after v0.0.2)
(Now using Godot **3.1.2.**)

### Added
* New GUI widgets. The idea here is to make existing "functional elements" (e.g., a set of related buttons) into self-contained scene widgets for easy use in project-specific GUI. This will be done on an as-needed basis.
   * SystemNavigator - NavigationPanel widget with the selectable sun/planets/moons.
   * ViewpointBox - SelectionPanel widget with Zoom/45/Top buttons
   * FocalLengthBox - SelectionPanel widget with focal-length label & buttons

### Changes
* Widget RangeLabel sets its own visibility

### API-breaking changes
* Renamed VoyagerCamera enum "VIEWPOINT_BUMPED_POINTING" -> "VIEWPOINT_BUMPED"
* Renamed widget "CameraRange" -> "RangeLabel"

### Bug fixes
* Fixed var shadowing error
