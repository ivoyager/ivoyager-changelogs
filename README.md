# current _master_ branch
Developed using **Godot 3.2.3** (ok in 3.2.4-rc1; there is a lighting problem in -rc2 that has been reported and fixed, so waiting to test -rc3)

Requires non-Git-tracked **ivoyager_assets-0.0.7**; find it in [ivoyager releases](https://github.com/ivoyager/ivoyager/releases).

See cloning and downloading instructions [here](https://ivoyager.dev/download/). 

See other recent changes in v0.0.8.md & v0.0.7.md.

## Added
* New IOManager manages a separate thread for I/O including resource loading and cache writing. Use IOManager.callback(object, io_method, finish_method, array) to get a callback on the I/O thread (for I/O or "I/O-adjacent" tasks such as resource loading and building parts of scene trees) and a subsequent callback on the Main thread (e.g., to attach results of previous work to the Scene Tree). If you set Global.enable_threads = false, everything still works but all on the Main thread.

## Changes
* We now have a dedicated I/O thread that does all resource loading and other I/O-adjacent tasks (such as building much of the solar system before attachment to the scene tree). Our solar system build was already fast but it's now blazingly fast! Unfortunately, we won't be able to use threads for the Web Planetarium until Godot 4.0.
* Universe is now replaceable in ProjectBuilder.

## API-breaking changes
* Save/load related functions moved from StateManager to new SaveLoadManager.
* Function name changes in StateManager: add_active_thread -> add_blocking_thread, remove_active_thread -> remove_blocking_thread.

## Bug fixes
* Fixes to mouse_filter in various GUIs (was preventing selection of Iapetus).
