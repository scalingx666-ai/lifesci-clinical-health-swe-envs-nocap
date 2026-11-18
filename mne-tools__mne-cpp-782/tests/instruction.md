# Issue

**Title:** [ENH, WIP] MNE_Analyze Dynamically reload plugins

## Description

Hi everybody,
This allows to, while the mne_analyze app is running, click a menu "File>Reload Plugins" and if new dlls is found in the plugin folder, the menus, views, controls will be loaded. 

- This is not WASM ready. Not sure how you could modify the plugin set during wasm execution.

While doing this I noticed a few problems with the actual application itself, not directly related but I think my changes do improve the code. 
- PluginManager stores the plugins in a specific order given by a ```m_iOrder``` variable that works as a hint on what position you want your plugin to appear. Depending on which order you set this var to be, and what other plugins decide, your plugin will appear higher or lower in the menus. 
- Some warnings have been addressed. ✊🏻 
- If a plugin has already been loaded it will be not loaded again to the PluginManager list. 
- When data is loaded to the PluginManager there is new AbstractPlugin flag:```m_bInitialized``` flag that reflects that state.
- When the plugin has had its ```menus```, ```Controls``` and ```Views``` loaded to the menus of the application's window, there will be three member flags to show that: ```m_bMenuAlreadyLoaded```, ```m_bControlAlreadyLoaded``` and  ```m_bViewAlreadyLoaded ```.
- Added `.cpp` file to AbstractPlugin.
- MainWindow was a global object (within MNEANALYZE ns). It is now owned by AnalyzeCore, and there is a global pointer that gets intitialized and can be looking at MainWindow. This is used for the globalLogger.
- AnalyzeCore would previously give access to pluginmanager to the GUI. I see no reason why this should be the case, since these are two completely different things. So now MainWindow and PluginManager both communicate with their controller (AnalyzeCore). 
- I saw a few ```onThatEvent``` type of methods/slots... I think that we should try to adopt a more imperative style. The user (a gui, in this case, for instance) uses an api of another class... so you just use it. So not react to an event, just use the class you are supposed to use. (example: ```OnMainWindowClose``` -> ```close``` as in The gui uses the function ```close``` provided by the MainWindow Object).

If you check the files, you'll find a few changes in Plugins themselves. I solve a few tiny typo/style problems in a few of them.

Still a few things to do, like: 
-  PluginManagers could generate a leak of the created menu objects if ```getMenus()``` is called more than once. Although This is not the responsibility of AbstractPlugin, at least don't think so.

## Task

Modify the repository so that the issue described above is resolved. The repository is checked out at base commit `cfa4bba73c8b`. Edit files in place; the verifier captures your changes via `git diff` and scores them against an oracle patch using SWE-RL-style diff-similarity reward.