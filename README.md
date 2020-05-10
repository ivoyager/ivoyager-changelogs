# _master_ branch
Godot version **3.2.1**.

Requires **ivoyager_assets-dev-2020-05-08** (updated for 0cce1d1): [download](https://github.com/ivoyager/ivoyager-changelogs/releases/download/dev-assets/ivoyager_assets-master-2020-05-08.zip)

* Note 1: There is a lot of API-breakage lately! I want to do that now before we go to official beta.
* Note 2: We changed the main scene to Universe! If you update the ivoyager submodule in your own project, you will need to change two settings in project.godot manually (I don't know why there are two! and for some reason, the 2nd doesn't update when changed from editor):
   * run/main_scene="res://ivoyager/tree_nodes/universe.tscn"
   * main_scene="res://ivoyager/tree_nodes/universe.tscn" (this one didn't update from the editor!)

### Added
* Added small moon 3d models: Phobos, Deimos, Hyperion (plus a couple asteroids but you can't visit these yet).
* More planetary data (surface atmos pressure, surface temp, etc.).
* Added static class UnitDefs (static/unit_defs.gd) that defines base and derived units, and all simulator internal representation. It provides constants, dictionaries and functions for unit conversion.
* Added class QtyStrings (program_refs/qty_strings.gd) for generating GUI quantity strings with units. User specifies display units and other options, but does not need to know sim internal units. For example, functions can be called to display an internal mass property in pure SI form "3.00x10^15 kg" or more sci-fi style "3.00 Terratonnes".
* Added class ~~TableHelper~~ TableReader (the old TableReader is now TableImporter). This class provides all table access.
* Added static class Enums (static/enums.gd). Moved enums here that are shared among multiple classes. (Enums used only in one class and its own function signatures still reside in the class.)
* Added Global signals: "about_to_exit", "about_to_quit".
* Added Timekeeper function to get real World GMT time (from user system clock). The Planetarium starts in "real world time" and can be reset to this in the time control GUI.
* Added 3 Global arrays for timekeeping (these supercede Global.time_array). You can grab and keep a reference to these in your class file header (e.g., var clock: Array = Global.clock):
   * Global.times = \[sim_time (SI seconds since J2000), engine_time (accumulated delta), UT1 days] (floats)
   * Global.date = \[year, month, day] (ints)
   * Global.clock = \[hour, minute, second] (ints)
* Added 4 "mouse drag modes" in BCameraInput (program_nodes/viewport_input.gd). There are project vars in ViewportInput that let you hook these up as you want, but by default we have:
   * Left mouse button drag: moves camera around the target body.
   * Shift + any mouse button drag: pitch, yaw
   * Alt + any mouse button drag: roll
   * Cntr + any mouse button OR right button drag: "hybrid" of above two (pitch, yaw if mouse near screen center; roll if near screen edge).
* Added smoothing for camera motions and rotations.
* Added "Universe" as the top Spatial and main scene root. We previously did a scene change after solar system build and when exiting, but now it just stays Universe at all times.
* Added new factory classes (all in ivoyager/program_refs/): EnvironmentBuilder, HUDsBuilder, ModelBuilder, LightBuilder.
* Added data table classes.csv with basic astronomical classifications like G-Type Star, Terrestrial Planet, Gas Giant, C-Type Asteroid, etc. Includes wiki_en title for url linking.
* SelectionData widget shows "classification" from classes.csv table above, and provides option to make these into Wikipedia links (off by default, but Planetarium sets to on).
* Added Body.flags and Enums.BodyFlags. Flag logic supercedes previous boolean members and selection_type (removed).
* Added Body components Rotations & Properties (new tree_ref classes). Together with Orbit, these define almost everything about Body.
* Implemented decimal precision. Table significant digits are maintained in display, even after import unit conversion and for derived values.
* For external project support, we now have a "fall-through" system for finding models, world maps, icons, body 2D images, and rings. See "search" arrays in Global.
* Added Global.is_gles2 (autodetects).
* Added Global.auto_exposure_enabled (project setting). EnvironmentBuilder sets from Global value.
* First attempt at HDR, auto-exposure, glow/bloom. EnvironmentBuilder, LightBuilder & ModelBuilder attempt to compensate for 3 different scenarios: 1. GLES2; 2. GLES3, auto_exposure_enabled = true; 3. GLES3, auto_exposure_enabled = false. 
### Changes
* Total makeover for Planetarium GUI.
* Recolored the fallback globe model for non-imaged bodies; now grey with whitish lat/long grid.
* Renamed all .csv data tables in data/solar_system/ directory (simplified to "planets.csv", etc.).
* External .csv data table row headers Data_Type, Default_Value & Unit_Conversion changed to DataType, Default & Units. Units row now takes strings such as "km", "au", "1/century", "10^24 kg", "km^3/s^2"; see static/unit_defs.gd for allowed symbols. Data tables no longer need to know sim internal units.
* Data tables accept new DataType 's to assist object building:
   * "DATA" - interpreted as row number (int) of item in any imported data table (e.g., CLASS_G_STAR).
   * "BODY" - interpreted as Body instance by that name (e.g., PLANET_EARTH).
   * Any enum name in the Enums static class (or replacement class specified in Global.enums) - interpreted as enum (int).
* A large chuck of BCamera code was split off into a new class: BCameraInput. The new class handles input not handled by InputHandler or various GUIs (what's left is camera movement control plus viewport click selection).
* BCamera is now fully replaceable with another Camera class in ProjectBuilder (i.e., you don't have to subclass BCamera). See comments in tree_nodes/b_camera.gd for tips on this (you'll still need to match some BCamera API and/or modify some other classes).
* BCamera can now traverse poles. Movement/rotation code is more comprehensible and robust (although a full overhaul to quaternions would be better than existing code).
* Improved distance selection when moving BCamera between bodies of different sizes.
* Lazy init for minor moon models (and uniniting for models not visited for a while). This cuts the number of models at any time from >130 to <30, which is a HUGE improvement for low end graphics computers!
* Directory program_refs split into prog_builders and prog_refs (the former are factory classes, the latter are runtime classes). Also renamed program_nodes -> prog_nodes.
### API-Breaking Changes
* Removed Global.scale (superseded by UnitDefs.METER). There may be other API breakages related to the units/scaling overhaul.
* All imported data table access is different. See class TableReader (program_refs/table_reader.gd) for table data access.
* Changed Global.enums. It was a dictionary. It now holds a reference to the actual Enums static class. The reason we have a reference in Global is so you can extend Enums class (with your own enums), set Global.enums to it, and then classes can find them (e.g., TableReader).
* Renamed Global.objects -> Global.program. (This holds single instance program_nodes & program_refs.)
* ~~Renamed Global.time_array -> Global.time_date~~ Global.time_array superceded; see Global.times, Global.date, Global.clock above. 
* Renamed Global signals; require_stop_requested -> sim_stop_required, allow_run_requested -> sim_run_allowed, about_to_add_environment -> environment_created
* Renamed Orbit.get_cartesian() -> get_vectors() & get_cartesian_from_elements() -> get_vectors_from_elements()
* Removed StringMaker. Replaced by more powerful QtyStrings.
* Renamed VoyagerCamera -> BCamera. (B for Body; presumably others will add "free flight" or other cameras.) Most of BCamera interface has changed.
* Changes to Timekeeper interface.
* Registrar.top_body changed to top_bodies (an array; contains only the Sun now but could contain, for example, a group of stars).
* Removed a bunch of "passive" tree_nodes classes that had only init() function: Model, HUDLabel, HUDIcon, Starlight, TempRings & VoyagerEnvironment. New "builder" classes generate the relevant base classes and add them as needed.
* Removed GUITop. (Universe is now the main scene at start and stays so after solar system build.)
* Renamed bodies.csv to models.csv (this table is about graphic representation of bodies).
* Removed Enums.SelectionTypes (and related members in Body and SelectionItem). Code cruft.
* Many Body boolean members are superceded by Body.flags.
* ProjectBuilder.program_refs dictionary was split into program_builders and program_refs (corresponding to directory changes listed above).
* Reorganized arrays & dicts that hold asset paths/directories in Global.
