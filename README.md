# master (after v0.0.1)

### Added
* Yaw, Pitch, Roll - via hotkeys and right-button mouse drag (drag near screen center for yaw/pitch, or near edge for roll)

### Interface-breaking changes
* Signature changes in SaverLoader.save_game() & load_game(); this is to make SaverLoader stand-alone so it can be added to Godot Asset Library.
* Moved make_object_or_scene() from FileHelper to SaverLoader; same reason as above.
* Some VoyagerCamera API to allow for yaw/pitch/roll rotations.

### Bug fixes
* fixed Credits button in exports (released in hotfix a)
