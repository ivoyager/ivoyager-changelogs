# _master_ branch
(Currently Godot version **3.1.2** but anticipating 3.2)

### Changes
* Improved Planetarium GUI visibility control. GUI won't disapear when mouse in margin between GUI and screen edge.
* Planetarium uses common MainMenu rather than its own menu. This allows add-ons or other external code to use MainMenu API to add buttons for Planetarium.
* Copyright notices updated for 2020.

# _godot-3.2_ branch
(Tested w/ Godot 3.2-beta5)

### Bug fixes
* Button signal fixes. (Not compatible with Godot 3.1.2.) (Edit: some button widgets broken again in beta6. Will wait for now and probably fix in Godot 3.2 release or release candidate.)
