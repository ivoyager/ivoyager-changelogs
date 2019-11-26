# v0.0.2

### Added
* Yaw, Pitch, Roll - via hotkeys and right-button mouse drag (drag near screen center for yaw/pitch, or near edge for roll)

### Changes
* Reduced window size to fit inside HD screen: now 1800 x 900. (This is in Project Settings so it will only effect new Project Templates and the stand-alone Planetarium.) It's still resizable.
* "Quit/Exit without saving?" confirmations disabled if save/load disabled.

### Interface-breaking changes
* Signature changes in SaverLoader.save_game() & load_game(); this is to make SaverLoader stand-alone so it can be added to Godot Asset Library.
* Moved make_object_or_scene() from FileHelper to SaverLoader (same reason as above).
* Some VoyagerCamera API changes to allow for yaw/pitch/roll rotations.

### Bug fixes
* Fixed Credits button in exports (released in hotfix a)
* Fixed InfoPanel movement when minimizing
* Removed non-existent hotkeys
