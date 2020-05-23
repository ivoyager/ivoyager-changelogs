# _master_ branch
(Godot version **3.2.1**)

Notes:
1. Requires **ivoyager_assets-0.0.6**: [download here](https://github.com/ivoyager/ivoyager/releases/download/v0.0.6-alpha/ivoyager_assets-0.0.6.zip).
2. Translations are now loaded from Global.translations for two reasons: a) so extensions can add w/out access to project.godot and b) for unicode support using \uHHHH escape code. If you're updating ivoyager submodule only, you should delete all localization files in the editor (i.e., from project.godot). Add them to Global.translations, via extension code at extension_init(), and reimport text.csv files with compress OFF (this is required only if you need unicode support).

## Changes
* Translations are loaded from Global.translations so extensions can add w/out access to project.godot.
* Unicode escape using \uHHHH (where HHHH is a hexidecimal value) can now be used in localized text and data tables. To make this work, text.csv files must be reimported with compress OFF. (This is a GDScript patch until Godot issue [#38716](https://github.com/godotengine/godot/issues/38716) gets fixed.)
* Changed .gitignore to allow tracking of export_presets.cfg in the project directories.
* HTML5 export projects close their own browser window on quitting.
