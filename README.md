[![Savior](https://i.imgur.com/fj3ZcYM.png)](https://www.unrealengine.com/marketplace/en-US/product/savior)

# Savior Plugin Documentation


| [Product Page](https://www.unrealengine.com/marketplace/en-US/product/savior) | [Community](https://forums.unrealengine.com/t/plugin-savior-3/110080) | [Contact](mailto:bruno_xavier_@msn.com) | [FAQ](#faqs) |
| ------- | ------- | ------- | ------- |
|   |   |   |   |

Savior is a C++ tool designed to extend Unreal's save system, providing a more powerful serialization framework for complex Unreal projects.
Savior is a custom serialization system built from scratch with efficiency in mind, together with a focus in productivity and ease-of-use in Unreal.
This documentation summarizes most common doubts of new users, most common mistakes, and the best solutions to achieve developer's goals.


## Features

| Productivity |
| ------------ |
| Savior eliminates micro-management of individual properties, becoming a valuable time saver for small teams.      |
| Marking a property with Unreal's 'Save Game' exposes property to the save system, no mirror property required.    |
| A rich library of helper functions brings free customization of the save process within blueprints, no coding.    |
| Deleting or adding new blueprint properties will not corrupt existing save files; Contrary to other save systems. |
| Built-in versioning system helps patching live games, without causing players to lose existing progress.          |

| Performance |
| ----------- |
| Savior abuses Unreal's multi-threading capabilities. Saving data is absurdly fast, only limited by target hardware. |
| Blueprint properties are read directly from target, mirror property in slots not required, increasing performance.  |
| Actor's location, rotation, scale, velocity, mesh, materials; Are all recorded from multi-threaded algorithms.      |

| Utility |
| ------- |
| Savior is based on *slots* to persist data. |
| A full HUD system ships with the plugin, making easy to implement loading screens, slot selection screens.        |
| Data loading progress is automatically calculated, generating feedback progress bars without developer efforts.   |


## Quick Guides

+ [Install Plugin](https://github.com/BrUnOXaVIeRLeiTE/Unreal-Savior.github.io/wiki/How-to-Install-Plugin "Savior Plugin Wiki")
+ [Creating Slots](https://forums.unrealengine.com/t/plugin-savior-3/110080/3 "Unreal Forums")
+ [Using Save Slots](https://forums.unrealengine.com/t/plugin-savior-3/110080/4 "Unreal Forums")
+ [Savior Tags System](https://forums.unrealengine.com/t/plugin-savior-3/110080/7 "Savior Forums")
+ [Auto-Destroy Mark](https://forums.unrealengine.com/t/plugin-savior-3/110080/5 "Unreal Forums")
+ [Runtime Spawned Actors](https://forums.unrealengine.com/t/plugin-savior-3/110080/6 "Unreal Forums")
+ [It's All About the *SGUID* Property](https://github.com/BrUnOXaVIeRLeiTE/Unreal-Savior.github.io/wiki/Understanding-SGUID "Savior Plugin Wiki")


## Advanced Guides
+ [Savior in C++](https://github.com/BrUnOXaVIeRLeiTE/Unreal-Savior.github.io/wiki/Savior-in-CPP "Savior Plugin Wiki")


## Savior API

### Asynchronous Methods:
+ [Load Game Instance (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameInstance/nodes/UK2Node_AsyncAction.html)
+ [Load Game Instance [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameInstance_Callback/nodes/UK2Node_AsyncAction.html)
+ [Load Game Mode (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameMode/nodes/UK2Node_AsyncAction.html)
+ [Load Game Mode [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameMode_Callback/nodes/UK2Node_AsyncAction.html)
+ [Load Game World (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameWorld/nodes/UK2Node_AsyncAction.html)
+ [Load Game World [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadGameWorld_Callback/nodes/UK2Node_AsyncAction.html)
+ [Load Level (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadLevel/nodes/UK2Node_AsyncAction.html)
+ [Load Level [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_LoadLevel_Callback/nodes/UK2Node_AsyncAction.html)
+ [Open Level (+HUD)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_OpenLevel/nodes/UK2Node_AsyncAction.html)
+ [Open Level (+HUD) [+Callback]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_OpenLevel_Callback/nodes/UK2Node_AsyncAction.html)
+ [Save Game Instance (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameInstance/nodes/UK2Node_AsyncAction.html)
+ [Save Game Instance [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameInstance_Callback/nodes/UK2Node_AsyncAction.html)
+ [Save Game Mode (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameMode/nodes/UK2Node_AsyncAction.html)
+ [Save Game Mode [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameMode_Callback/nodes/UK2Node_AsyncAction.html)
+ [Save Game World (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameWorld/nodes/UK2Node_AsyncAction.html)
+ [Save Game World [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveGameWorld_Callback/nodes/UK2Node_AsyncAction.html)
+ [Save Level (Async)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveLevel/nodes/UK2Node_AsyncAction.html)
+ [Save Level [+Callbacks]](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_SaveLevel_Callback/nodes/UK2Node_AsyncAction.html)

### Slot Methods:
+ [Synchronous Slot Methods](https://brunoxavierleite.github.io/Savior2API.github.io/Savior3/Savior3.html)

### Serializable Interface:
+ [Event: On Loaded](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnLoaded.html)
+ [Event: On Marked (Auto-Destroy)](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnMarkedAutoDestroy.html)
+ [Event: On Prepare To Load](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnPrepareToLoad.html)
+ [Event: On Prepare To Save](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnPrepareToSave.html)
+ [Event: On Saved](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Serializable/nodes/OnSaved.html)

### Procedural Interface:
+ [Event: On Begin Respawn](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Procedural/nodes/OnBeginRespawn.html)
+ [Event: On Finish Respawn](https://brunoxavierleite.github.io/Savior2API.github.io/SAVIOR_Procedural/nodes/OnFinishRespawn.html)

### HUD Class:
+ [Event: On Begin Load-Screen](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/OnBeganLoadScreen.html)
+ [Event: On Finish Load-Screen](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/OnFinishedLoadScreen.html)
+ [Invoke Load Screen (Blur)](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/DisplayBlurLoadScreenHUD.html)
+ [Invoke Load Screen (Splash)](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/DisplaySplashLoadScreenHUD.html)
+ [Remove Load Screen](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/RemoveLoadScreen.html)
+ [Hide Slots UI](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/HideSlotPickerHUD.html)
+ [Show Slots UI](https://brunoxavierleite.github.io/Savior2API.github.io/HUD_SaviorUI/nodes/ShowSlotPickerHUD.html)


## FAQs

> How, why my Actor isn't saving?

Chances are you did not setup a [*SGUID* Property](https://github.com/BrUnOXaVIeRLeiTE/Unreal-Savior.github.io/wiki/Understanding-SGUID "Savior Plugin Wiki") properly.

> Save World or Game Mode returns *Failed* result, why?

Check thread state with [Get Thread Safety](https://github.com/BrUnOXaVIeRLeiTE/Unreal-Savior.github.io/wiki/Understanding-SGUID "Savior Plugin Wiki") node. If you have another save process running, you have to wait until previous process is complete to start a new one.

> I still can't save anything?!

Make sure you are creating an instance with [New Slot Instance](https://i.imgur.com/lxQhI3V.png) node. Don't try to save data directly into your Slot Class.