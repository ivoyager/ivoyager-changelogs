# master (post v0.0.1)

### Interface-breaking changes
* Signature changes in SaverLoader.save_game() & load_game(); this is to make SaverLoader stand-alone so it can be added to Godot Asset Library.
* Moved make_object_or_scene() from FileHelper to SaverLoader; same reason as above.

### Bugs
* fixed Credits button in exports (hotfix a)
