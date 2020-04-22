# _master_ branch
Godot version **3.2.1**.

Requires **ivoyager_assets-dev-2020-04-13**: [download](https://github.com/ivoyager/ivoyager-changelogs/releases/download/dev-assets/ivoyager_assets-dev-2020-04-13.zip) (Older release 0.0.5 ivoyager_assets won't work!)

Notes: There is a lot of API-breakage lately - I want to do that now before we go to official beta! There is also a new graphic "hang" that happens exactly at the half-way point of a camera movement (almost certainly coincident with camera changing parents). It could be related to the new 3d models, or to Godot 3.2.x update, or something I screwed up in the code... 

### Added
* Added small moon 3d models: Phobos, Deimos, Hyperion (plus a couple asteroids but you can't visit these yet).
* More planetary data (surface atmos pressure, surface temp, etc.) is imported into Body object. This is shown in Project Template but not (yet) in Planetarium. (I need to add a new "body info" popup for the Planetarium.)
* Added static class UnitDefs (static/unit_defs.gd) that defines base and derived units, and all simulator internal representation. It provides constants, dictionaries and functions for unit conversion.
* Added class QtyStrings (program_refs/qty_strings.gd) for generating GUI quantity strings with units. User specifies display units and other options, but does not need to know sim internal units. For example, functions can be called to display an internal mass property in pure SI form "3.00x10^15 kg" or more sci-fi style "3.00 Terratonnes".
* Added class TableHelper (program_refs/table_helper.gd). Look here to understand the new imported table encoding.
* Added static class Enums (static/enums.gd). Moved enums here that are shared among multiple classes. (Enums used only in one class and its own function signatures still reside in the class.)
* Added Global signals: "about_to_exit", "about_to_quit".
* Real World GMT time (from user system clock). The Planetarium starts in "real world time" and can be reset to this in the time controls.
### Changes
* Recolored the fallback globe model for non-imaged bodies; now grey with whitish lat/long grid.
* Renamed all .csv data tables in data/solar_system/ directory.
* External .csv data table row headers Default_Value & Unit_Conversion changed to Defaults & Units. Units row now takes strings such as "km", "au", "1/century", "10^24 kg", "km^3/s^2"; see static/unit_defs.gd for allowed symbols. Data tables no longer need to know sim internal units.
* A large chuck of BCamera code was split off into a new class: ViewportInput. The new class handles input not handled by InputHandler or various GUIs (what's left is camera movement control plus viewport click selection).


### API-Breaking Changes
* Removed Global.scale (superseded by UnitDefs.METER). There may be other API breakages related to the units/scaling overhaul.
* All imported data table access is different. See class TableHelper for how to get data from row/column identifiers. Global.tables & Global.table_types were replaced by Global.table_data, Global.table_fields & Global.table_rows.
* Changed Global.enums. It was a dictionary. It now holds a reference to the actual Enums static class.
* Renamed Global.objects -> Global.program. (This holds single instance program_nodes & program_refs.)
* Renamed Global.time_array -> Global.time_date
* Renamed Global signals; require_stop_requested -> sim_stop_required, allow_run_requested -> sim_run_allowed
* Renamed Orbit.get_cartesian() -> get_vectors() & get_cartesian_from_elements() -> get_vectors_from_elements()
* Removed StringMaker. Replaced by more powerful QtyStrings.
* Renamed VoyagerCamera -> BCamera. (B for Body; presumably others will add "free flight" or other cameras.) Most of BCamera interface has changed.
* Renamed VoyagerEnvironment -> VEnv.

