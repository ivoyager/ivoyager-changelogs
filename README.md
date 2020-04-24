# _master_ branch
Godot version **3.2.1**.

Requires **ivoyager_assets-dev-2020-04-13**: [download](https://github.com/ivoyager/ivoyager-changelogs/releases/download/dev-assets/ivoyager_assets-dev-2020-04-13.zip) (Older release 0.0.5 ivoyager_assets won't work due to changes in the asteroid binaries.)

Notes: There is a lot of API-breakage lately - I want to do that now before we go to official beta! There is also a new graphic "hang" that happens exactly at the half-way point of a camera movement (almost certainly coincident with camera changing parents). It could be related to the new 3d models, or to Godot 3.2.x update, or something I screwed up in the code... 

### Added
* Added small moon 3d models: Phobos, Deimos, Hyperion (plus a couple asteroids but you can't visit these yet).
* More planetary data (surface atmos pressure, surface temp, etc.).
* Added static class UnitDefs (static/unit_defs.gd) that defines base and derived units, and all simulator internal representation. It provides constants, dictionaries and functions for unit conversion.
* Added class QtyStrings (program_refs/qty_strings.gd) for generating GUI quantity strings with units. User specifies display units and other options, but does not need to know sim internal units. For example, functions can be called to display an internal mass property in pure SI form "3.00x10^15 kg" or more sci-fi style "3.00 Terratonnes".
* Added class TableHelper (program_refs/table_helper.gd). Look here to understand the new imported table encoding.
* Added static class Enums (static/enums.gd). Moved enums here that are shared among multiple classes. (Enums used only in one class and its own function signatures still reside in the class.)
* Added Global signals: "about_to_exit", "about_to_quit".
* Added Timekeeper function to get real World GMT time (from user system clock). The Planetarium starts in "real world time" and can be reset to this in the time control GUI.
* Added 3 Global arrays for timekeeping (these supercede Global.time_array). You can grab and keep a reference to these in your class file header (e.g., var clock: Array = Global.clock):
   * Global.times = \[sim_time (SI seconds since J2000), engine_time (accumulated delta), UT1 days] (floats)
   * Global.date = \[year, month, day] (ints)
   * Global.clock = \[hour, minute, second] (ints)
* Added 4 "mouse drag modes" in ViewportInput (program_nodes/viewport_input.gd). There are project vars in ViewportInput that let you hook these up as you want, but by default we have:
   * Left mouse button drag: moves camera around the target body.
   * Shift + any mouse button drag: pitch, yaw
   * Alt + any mouse button drag: roll
   * Cntr + any mouse button OR right button drag: "hybrid" of above two (pitch, yaw if mouse near screen center; roll if near screen edge).
### Changes
* Total makeover for Planetarium GUI.
* Recolored the fallback globe model for non-imaged bodies; now grey with whitish lat/long grid.
* Renamed all .csv data tables in data/solar_system/ directory (simplified to "planets.csv", etc.).
* External .csv data table row headers Default_Value & Unit_Conversion changed to Defaults & Units. Units row now takes strings such as "km", "au", "1/century", "10^24 kg", "km^3/s^2"; see static/unit_defs.gd for allowed symbols. Data tables no longer need to know sim internal units.
* A large chuck of BCamera code was split off into a new class: ViewportInput. The new class handles input not handled by InputHandler or various GUIs (what's left is camera movement control plus viewport click selection).
* BCamera is now fully replaceable with another Camera class in ProjectBuilder (ie, you don't have to subclass BCamera). See comments in tree_nodes/b_camera.gd for tips on this (you'll still need to match some BCamera API and/or modify some other classes).
### API-Breaking Changes
* Removed Global.scale (superseded by UnitDefs.METER). There may be other API breakages related to the units/scaling overhaul.
* All imported data table access is different. See class TableHelper for how to get data from row/column identifiers. Global.tables & Global.table_types were replaced by Global.table_data, Global.table_fields & Global.table_rows.
* Changed Global.enums. It was a dictionary. It now holds a reference to the actual Enums static class.
* Renamed Global.objects -> Global.program. (This holds single instance program_nodes & program_refs.)
* ~~Renamed Global.time_array -> Global.time_date~~ Global.time_array superceded; see Global.times, .date, .clock above. 
* Renamed Global signals; require_stop_requested -> sim_stop_required, allow_run_requested -> sim_run_allowed
* Renamed Orbit.get_cartesian() -> get_vectors() & get_cartesian_from_elements() -> get_vectors_from_elements()
* Removed StringMaker. Replaced by more powerful QtyStrings.
* Renamed VoyagerCamera -> BCamera. (B for Body; presumably others will add "free flight" or other cameras.) Most of BCamera interface has changed.
* Renamed VoyagerEnvironment -> VEnv.
* Changes to Timekeeper interface.
