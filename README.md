# _master_ branch
Godot version **3.2.1**.

Requires **ivoyager_assets-dev-2020-04-13**: [download](https://github.com/ivoyager/ivoyager-changelogs/releases/download/dev-assets/ivoyager_assets-dev-2020-04-13.zip)

### Changes
* Added small moon 3d models: Phobos, Deimos, Hyperion.
* Recolored the fallback globe model for non-imaged bodies; now grey with whitish lat/long grid.
* Overhauled measurement units & sim scaling:
  * Added static class UnitDefs (static/unit_defs.gd) that defines base and derived units, and all simulator internal representation. It provides constants, dictionaries and functions for unit conversion.
  * Added class QtyStrings (program_refs/qty_strings.gd) for generating GUI quantity strings with units. User specifies display units and other options, but does not need to know sim internal units. For example, functions can be called to display an internal mass property in pure SI form "3.00x10^15 kg" or more sci-fi style "3.00 Terratonnes".
* Overhauled imported data table structures:
  * External .csv data table row headers Default_Value & Unit_Conversion changed to Defaults & Units. Units row now takes strings such as "km", "au", "1/century", "10^24 kg", "km^3/s^2"; see static/unit_defs.gd for allowed symbols. Data tables no longer need to know sim internal units.
  * Added Global.table_types dictionary. This gives enum-like access to imported data table "types" (type = row number integer) by "key". You can access the type by key directly (moon_type = Global.table_types.MOON_EUROPA) or via individual table dicts (moon_type = Global.table_types.MoonTypes.MOON_EUROPA).
  * In the Global.tables dictionary, we now have 1 array (of arrays) and 1 dict for each imported table. For example, we have MoonData and MoonFields. Combining w/ above change, you would get a data entry (e.g., Europa's albedo) as follows:
```
var moon_type: int = Global.table_types.MOON_EUROPA # or tabel_types.MoonTypes.MOON_EUROPA
var albedo_field: int = Global.tables.MoonFields.albedo #  it's different in PlanetFields!
var europa_data: Array = Global.tables.MoonData[moon_type]
var albedo = europa_data[albedo_field]
```
* Added static class Enums (ivoyager/static/enums.gd). Moved enums here that are shared among multiple classes. (Enums used only in a class and its own function signatures still reside in the class.)
* Added Global signals: "about_to_exit", "about_to_quit"
### API-Breaking Changes
* Removed Global.scale (superseded by UnitDefs.METER). There may be other API breakages related to the units/scaling overhaul.
* All data table access (see overhaul above).
* Removed Global.enums. Previous contents moved to either Enums class or Global.table_types.
* Renamed Global.objects -> Global.program. (This holds single instance program_nodes & program_refs.)
* Renamed Global.table_data -> Global.tables
* Renamed Global.time_array -> Global.time_date
* Renamed Global signals; require_stop_requested -> sim_stop_required, allow_run_requested -> sim_run_allowed
* Renamed Orbit.get_cartesian() -> get_vectors() & get_cartesian_from_elements() -> get_vectors_from_elements()
* Removed StringMaker. Replaced by more powerful QtyStrings.

