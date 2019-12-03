# master (after v0.0.2)
(Now using Godot **3.1.2.**)

### Added
* New GUI widgets. The idea here is to make existing "functional elements" (e.g., a set of related buttons) into self-contained scene widgets for easy use in project-specific GUI. This will be done on an as-needed basis.
   * SystemNavigator - NavigationPanel widget with the selectable sun/planets/moons.
   * ViewpointBox - SelectionPanel widget with Zoom/45/Top buttons.
   * FocalLengthBox - SelectionPanel widget with focal-length label & buttons.
   * CameraLock - NavigationPanel widget that locks/unlocks camera to main UI selection.

### Changes
* Widget RangeLabel sets its own visibility
* Renamed COPYRIGHT.txt to 3RD_PARTY.txt in all repositories. The file name "COPYRIGHT" interferes with GitHub's autoscript recognition of our Apache 2.0 license in LICENSE.txt.

### API-breaking changes
* Renamed VoyagerCamera enum "VIEWPOINT_BUMPED_POINTING" -> "VIEWPOINT_BUMPED"
* Renamed widget "CameraRange" -> "RangeLabel"

### Bug fixes
* Fixed var shadowing error
