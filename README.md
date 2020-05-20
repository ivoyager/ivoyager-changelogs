# _master_ branch
(Godot version **3.2.1**)

Notes:
1. Requires **ivoyager_assets-0.0.6**: [download](https://github.com/ivoyager/ivoyager/releases/download/v0.0.6-alpha/ivoyager_assets-0.0.6.zip)
2. Translations are now loaded from Global.translations so extensions can add w/out access to project.godot. If you're updating ivoyager submodule only, you should delete all localization files in the editor.

## Changes
* Translations are loaded from Global.translations so extensions can add w/out access to project.godot.
* "\uHHHH" can now be used in localization files and data tables for unicode characters (where "HHHH" is a hexidecimal value). For localization files, you must set "compress=false" in the .import file (it'll be compressed internally after "\uHHHH" unescape). This is a GDScript patch until Godot issue #38716 gets fixed.
