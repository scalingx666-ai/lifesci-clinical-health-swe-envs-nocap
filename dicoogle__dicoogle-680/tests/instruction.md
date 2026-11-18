# Issue

**Title:** Fix Web UI Plugin Settings Files Not Handled Properly / Include PatientID in study view entries

## Description

This PR fixes a broken feature of the web UI plugins' config files. Settings files are now properly loaded and provided to the respective web UI plugins. 

Additionally, study entries in the UI will now have the associated Patient ID included, for additional context.

## Description
Configurations for a web UI plugin have always been properly handled, so long as the files 
 (which must be named `[WebUIPluginName].json`, see `package.json`'s `name` attribute) are stored in `Plugins/settings`. However, neither the Web UI servlet nor `dicoogle-webcore.js` do any effort to provide or handle the settings so that web UI plugins can access these.

This PR modifies the web UI servlet to include a new `settings` parameter, having the contents of the settings file, should it exist. Furthermore, the webcore was updated to include a new `Settings` field in registered plugins. This allows default webplugin classes to access this field by simply referring to their own attributes (i.e.: `this.Settings`) during the `render(...)` method.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `57ebdcfa261a`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.