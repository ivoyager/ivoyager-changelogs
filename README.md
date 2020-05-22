# _master_ branch
(Godot version **3.2.1**)

Notes:
1. Requires **ivoyager_assets-0.0.6**: [download here](https://github.com/ivoyager/ivoyager/releases/download/v0.0.6-alpha/ivoyager_assets-0.0.6.zip).
2. Translations are now loaded from Global.translations for two reasons: 1) so extensions can add w/out access to project.godot and 2) for unicode escape ("\uHHHH") support. If you're updating ivoyager submodule only, you should delete all localization files in the editor (i.e., from project.godot). Add them to Global.translations (via extension code at extension_init()) and reimport text.csv files with compress OFF (the last item required for \uHHHH support).

## Changes
* Translations are loaded from Global.translations so extensions can add w/out access to project.godot.
* "\uHHHH" can now be used in localized text and data tables for unicode characters (where "HHHH" is a hexidecimal value). For localization files, you must set "compress=false" in the .import file (it'll be compressed internally after "\uHHHH" unescape). This is a GDScript patch until Godot issue [#38716](https://github.com/godotengine/godot/issues/38716) gets fixed.
* Changed .gitignore to allow tracking of export_presets.cfg in the project directories.
* HTML5 export projects close their own browser window on quitting.
