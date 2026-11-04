# Umapyoi Engine

A custom **C++20 / OpenGL** 2D game engine and level editor, and the action game built on it. It was made by a team of six students over a year-long DigiPen game project (CSD2401 / CSD2451).

The game is a top-down elemental action game. You fight Fire, Water and Wind demons with three elemental attacks, each one strong against a different enemy type. You can also chain two elements into a **fusion skill**. Basic skills cost mana and fusion skills cost more. The game runs from a tutorial through three levels to a three-phase boss fight, with cutscenes, dialogue, a shop and an online leaderboard along the way.

> This repository is a clean snapshot of the team's original private project, republished for portfolio purposes. The commit history was not carried over. The contributions of each member are summarised below.

---

## Features

### Engine
- **Entity Component System**: a central `Coordinator` over the entity, component and system managers, with signature-based system filtering, parent-child hierarchies, deferred deletion and play-mode state caching.
- **Rendering**: an OpenGL renderer with sprite batching and instanced drawing, sprite sheets and offsets, a material and effect-shader system, **2D lighting**, a particle system, sprite animation, FreeType text and a debug-draw layer.
- **Lua scripting** through Sol2. Gameplay is written in Lua scripts attached to entities, and those scripts can reach transforms, physics, sprites, audio, input, UI, scenes and PlayFab.
- **Physics and collision**: rigid bodies, colliders, projectiles and tilemap collision.
- **Audio**: an FMOD-based sound manager with audio components, a listener, grouped SFX and music, and a low-pass filter for post-processing.
- **AI**: a finite state machine system and grid pathfinding.
- **Events**: a hybrid observer event system with predicate-based filtering and automatic subscription management.
- **UI framework**: canvas, rect transforms, buttons, sliders, checkboxes, text, images and dialogue boxes, with keyboard, mouse and **controller** navigation.
- **Engine services**: a resource manager that auto-loads assets, a scene manager with async loading, JSON serialization (RapidJSON) for scenes and prefabs, cutscenes, a crash logger, a debugger and a debug memory manager.
- **Online**: PlayFab integration for player login, leaderboards and admin tools.

### Editor (`UmapyoiEditor`)
- Docked ImGui editor with hierarchy, inspector, console, scene view and game view.
- Entity picking and **translate / rotate / scale gizmos**.
- **Undo/redo** through a command pattern covering create, delete, duplicate, reparent, reorder, add/remove component and snapshot edits.
- File browser with drag and drop, asset previews and prefab save/load.
- Tilemap editor, resources window, PlayFab admin panel and a build-size analyzer.

### Game (`UmapyoiGame`)
- **Elemental combat**: Fire Slash, Water Slash and Wind Dash, plus three fusion skills: **Pyronado** (fire + wind), **Steam Burst** (fire + water) and **Whirlpool** (water + wind).
- Fire, Water and Wind demon enemies driven by state machines, elite variants, a bird enemy, and a **three-phase boss** with totems and bullet-hell patterns.
- Tutorial with dialogue, intro and ending cutscenes, checkpoints, a shop, a HUD with health, mana and cooldowns, and a PlayFab leaderboard.
- Full controller support.

---

## Team & Contributions

| Member | Main areas |
|---|---|
| **Leong Wai Men** ([beatsmoon](https://github.com/beatsmoon)) | Engine architecture, ECS, Lua scripting, physics, serialization, editor undo/redo, PlayFab, tilemaps, controller support |
| **Javier Chua Dong Qing** ([Siestasies](https://github.com/Siestasies)) | Graphics pipeline, window, animation, particles, 2D lighting, materials and shaders, editor camera, cutscenes |
| **Jedrek Lee Jing Wei** | Event system, math library, editor picking and gizmos, UI framework, HUD and menus |
| **Koh Kai Yang** | Audio system, FSM system, pathfinding, enemy AI scripts |
| **Shahir Rasid** | Scene manager, ImGui editor framework, level flow, triggers, shop |
| **Lai Jun Siang** ([JunSiangLai](https://github.com/JunSiangLai)) | Debug tooling, crash logger, memory manager, file browser, player and boss gameplay |

### Leong Wai Men: Engine architecture and core systems
- Designed the **engine core** (`Application`, `EngineConfig`, the game and editor application entry points) and the **ECS** (`Coordinator`, `EntityManager`, `ComponentManager`, `SystemManager`), including hierarchies, enable/disable and play-mode state caching.
- Wrote most of the core **components and systems**: transform, rigid body, collider, sprite, player, enemy, projectile, tilemap, camera, physics, collision, projectile, transform and rendering.
- Built the **Lua scripting system** (`LuaScriptingSystem`) and the scripting API exposed to gameplay code, and wrote its documentation.
- Implemented **serialization** for scenes, prefabs and engine config (`BaseSerializer`, `GameSerializer`, `EngineConfigSerializer`).
- Built the editor's **command pattern and undo/redo** (`CommandHistory` and the entity create, delete, duplicate, reparent, reorder, set-active and snapshot commands).
- Integrated **PlayFab** (player login, leaderboards and the admin API) and its editor panel.
- Built the **tilemap editor**, the **resource manager** and resources window, and the **build-size analyzer**.
- Added **controller input** and menu navigation, and co-wrote the player controller.
- Scripted many menu screens, the Fire, Wind and Water demon base behaviours, the bird enemy and enemy health bars.

### Javier Chua Dong Qing: Graphics, animation and effects
- Built the **OpenGL graphics layer** (`Graphics`) and **window management** (`Window`), and co-wrote the **input system**.
- Implemented the **sprite animation** pipeline (`Animator`, `SpriteAnimator`, `AnimatorSystem`), including sprite sheets, multiple sheets per sprite, UV cutting, sprite offsets and flip.
- Built the **particle system** (`ParticleEmitter`, `ParticleSystem`), including particle layering.
- Built **2D lighting** (`Light2D`, `SceneLighting`, `LightSystem`).
- Built the **material system** (`SpriteMaterial`) and effect shaders, plus colour tinting.
- Built the **editor camera** and **camera shake**.
- Built the **cutscene system** and scripted the cutscene triggers, death screen and how-to-play popups.
- Moved shaders, fonts and textures into the resource manager, added auto-loading, and wired up FreeType font rendering.
- Added the editor's **add/remove component** undo commands and the file browser's icons and image previews.
- Set up the original CMake project and dependencies, and handled lighting and setup on several levels.

### Jedrek Lee Jing Wei: Events, editor tools and UI
- Designed the **event system** (`EventSystem`): a hybrid observer design with predicate-based filtering, automatic subscription management, and the engine's event types (input, ECS, editor, audio, UI, scene and others).
- Wrote the **math library**: GLM-compatible 2D/3D vectors and 2x2, 3x3 and 4x4 matrices.
- Built the editor's **picking, gizmos and transform manipulation** (`EditorSystem`, `PickingSystem`, `GizmoRenderer`, `TransformManipulator`).
- Built the **UI framework** (`UISystem`, `Canvas`, `RectTransform`, `Button`, `Slider`, `Checkbox`, `Text`, `Image`, `Dialogue`, `Layout`) and the **hybrid input system** with input filtering.
- Built the **feedback system** (`FeedbackSystem`) for gameplay feedback effects.
- Co-wrote the player controller.
- Scripted the HUD (health, mana and cooldowns), the options menu with volume sliders, the in-game menus, the dialogue triggers and stage transitions.

### Koh Kai Yang: Audio and AI
- Built the **audio system** (`SoundManager`, `AudioSystem`, `AudioComponent`, `AudioListener`), with music and SFX groups, volume control and a low-pass post-processing filter. Also integrated the game's sound effects and music.
- Built the **finite state machine system** (`FSM`, `FSMSystem`) that the enemy and player state scripts run on.
- Implemented **pathfinding** (`PathFinding`, `PathFindingSystem`, `GridPathfinder`).
- Scripted **enemy AI**: the idle, chase, attack, stunned and death states for Fire, Water and Wind demons, including the Water Demon's self-destruct attack, plus the reusable state templates.
- Scripted the ending sequence and the cheat codes.

### Shahir Rasid: Scenes, editor framework and game flow
- Built the **scene manager** (`SceneManager`, `SceneType`) and the scene scripts that drive the editor and game.
- Built the **ImGui editor framework** (`ImguiManager`): docking layout, the entity debug and console windows, and the editor's styling.
- Built the engine's **system manager** (`SystemManager`, `SystemType`).
- Scripted the **level flow**: tutorial and level triggers, the level-end sequence, fades, the **shop**, the boss health bar and background music.

### Lai Jun Siang: Tooling and player gameplay
- Built the **debugger**, **crash logger** and debug **memory manager** used to track logs, crashes and leaks.
- Built the editor **file browser** (`FileSystem`) with drag and drop (`DropCallback`), prefab save/load and auto-refresh, and worked on the hierarchy and inspector windows.
- Scripted the **player** state machine: idle, run, dash, hurt, death and the elemental attacks and fusion skills (Fire Slash, Water Slash, Wind Dash, Pyronado, Steam Burst and Whirlpool).
- Scripted the **boss** and its three phases, the totems, checkpoints and the Kappa statue.

---

## Building

**Requirements:** Windows, Visual Studio 2022 or 2026 (x64), CMake 3.5 or later, and Git. A C++20 compiler is needed.

The easiest way is to run `run.bat`. It configures the project, asks which target (game, editor or both) and configuration to build, then launches the result.

To build manually:

```bat
mkdir build && cd build
cmake .. -G "Visual Studio 17 2022" -A x64
cmake --build . --target UmapyoiGame --config Release
```

CMake downloads the dependencies (GLFW, GLM, stb, Lua 5.4.6, Sol2 and the PlayFab SDK). FMOD, FreeType, GLAD, ImGui and RapidJSON are included in the repository. A post-build step copies `Assets/`, `Configs/` and the required DLLs next to the executable.

**PlayFab:** `Configs/playfab_dev.json` holds the PlayFab title ID. The developer secret key has been removed, so the editor's admin tools are disabled. Player login and leaderboards only need the title ID.

## Controls

| Action | Keyboard | Controller |
|---|---|---|
| Move | W A S D | Left stick |
| Water Slash | J | Y |
| Fire Slash | K | B |
| Wind Dash | L | A |
| Fusion skill | Press a second element during an elemental attack | Same |
| Advance dialogue / cutscene | Space / Enter / Left mouse | A |
| Pause | Esc | Start |

---

## Third-party

- [GLFW](https://www.glfw.org/), [GLM](https://github.com/g-truc/glm), [GLAD](https://glad.dav1d.de/), [stb](https://github.com/nothings/stb)
- [Lua 5.4](https://www.lua.org/) and [Sol2](https://github.com/ThePhD/sol2)
- [Dear ImGui](https://github.com/ocornut/imgui)
- [FMOD](https://www.fmod.com/) (FMOD Studio by Firelight Technologies Pty Ltd)
- [FreeType](https://freetype.org/)
- [RapidJSON](https://rapidjson.org/)
- [PlayFab SDK](https://playfab.com/)
- [SDL GameControllerDB](https://github.com/mdqinc/SDL_GameControllerDB)

All third-party libraries and assets belong to their respective owners.

## Academic notice

This project was created as coursework for CSD2401 and CSD2451 at **DigiPen Institute of Technology Singapore**.
All content © 2025 DigiPen Institute of Technology Singapore. All rights reserved.
