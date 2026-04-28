
<h1>
  <img src="https://github.com/mehah/otclient/blob/main/data/images/clienticon.png?raw=true" width="32" alt="logo"/>
  OTClient - Redemption - GunzOT compatible
</h1>

[![Discord Shield](https://discordapp.com/api/guilds/888062548082061433/widget.png?style=shield)](https://discord.gg/tUjTBZzMCy)
[![Build - Ubuntu](https://github.com/mehah/otclient/actions/workflows/build-ubuntu.yml/badge.svg)](https://github.com/mehah/otclient/actions/workflows/build-ubuntu.yml)
[![Build - Windows](https://github.com/mehah/otclient/actions/workflows/build-windows.yml/badge.svg)](https://github.com/mehah/otclient/actions/workflows/build-windows.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## <a id="table-of-contents"></a>📋 Table of Contents
1. ![Logo](https://raw.githubusercontent.com/mehah/otclient/main/src/otcicon.ico)  [What is OTClient?](#what-is-otclient)
2. 🚀 [Features](#features)
3. <img height="16" src="https://raw.githubusercontent.com/github/explore/80688e429a7d4ef2fca1e82350fe8e3517d3494d/topics/android/android.png"/> [The Mobile Project](#the-mobile-project)
4. 🔨 [Compiling](#compiling)
5. 🐳 [Docker](#docker)
6. 🩺 [Need Help?](#need-help)
7. 📑 [Bugs](#bugs)
8. ❤️ [Roadmap](#roadmap)
9. 💯 [Support Protocol](#support-protocol)
10. ©️ [License](#license)
11. ❤️ [Contributors](#contributors)

---

## <a id="what-is-otclient"></a>![Logo](https://raw.githubusercontent.com/mehah/otclient/main/src/otcicon.ico) What is OTClient?
OTClient is an alternative Tibia client for usage with OTServ. It aims to be **complete** and **flexible**:

- **LUA scripting** for all game interface functionality
- **CSS-like syntax** for UI design
- **Modular system**: each functionality is a separate module, allowing easy customization
- Users can create new mods and extend the interface
- Written in **C++20** and heavily scripted in **LUA**

For a server to connect to, you can build your own with **theforgottenserver** or **canary**.

> [!NOTE]
> Based on [edubart/otclient](https://github.com/edubart/otclient) • Rev: [2.760](https://github.com/edubart/otclient/commit/fc39ee4adba8e780a2820bfda66fc942d74cedf4)

---

## <a id="features"></a>🚀 Features

Beyond its flexibility with scripts, OTClient comes with many features that enable client-side innovation in OTServ: **sound system**, **graphics effects with shaders**, **modules/addons**, **animated textures**, **styleable UI**, **transparency**, **multi-language**, **in-game LUA terminal**, and an **OpenGL 2.0 ES engine** that allows porting to mobile platforms. It is also flexible enough to create Tibia tools like map editors using scripts—OTClient is a **framework + Tibia APIs**.

### ⚡ Performance & Engine
<details>
  <summary>🖼️ Draw Render (optimization showcase)</summary>

  https://github.com/user-attachments/assets/fe5f1d7f-7195-4d65-bca6-c2b5d62d3890
</details>

<details>
  <summary>📦 Asynchronous Texture Loading</summary>

- **Description**: with this the spr file is not cached, consequently, less RAM is consumed.
- **Video**:

  https://github.com/kokekanon/otclient.readme/assets/114332266/f3b7916a-d6ed-46f5-b516-30421de4616d
</details>

<details>
  <summary>🧵 Multi-threading</summary>

**Main Thread**
- Sound
- Particles
- Load Textures (files)
- Windows Events (keyboard, mouse, ...)
- Draw texture

**Thread 2**
- Connection
- Events (g_dispatcher)
- Collect information on what will be drawn on the Map

**Thread 3**
- Collect information on what will be drawn in the UI

**Image:**  
![multinucleo](https://github.com/kokekanon/otclient.readme/assets/114332266/95fb15ac-553f-4eca-937d-8c8f49990f3e)
</details>

<details>
  <summary>🧹 Garbage Collection</summary>

**Description (1):**
```
Garbage Collection is the feature responsible for automatically managing memory by identifying and releasing objects that are no longer in use. This allows the client to maintain efficient memory usage, avoid unnecessary data accumulation, and improve overall stability.
```

**Description (2):**  
Garbage collector is used to check what is no longer being used and remove it from memory. *(lua, texture, drawpool, thingtype)*
</details>

<details>
  <summary>🧭 Texture Atlas System</summary>

*(coming with engine improvements and draw-call reduction)*
</details>

- C++20 ( v17 , Unity build and Manifest Mode *(vcpkg.json)* ) build in x32 and x64  
- Walking System Improvements  
- Supports sequenced packages and compression  
- Asserts load (Tibia 13)

---

### 🎛️ UI & UX
<details>
  <summary>🧩 UIWidgets Improvements</summary>

- **Description:** Improvements in the UI algorithm; better performance in add/remove/reposition widgets. Visible in the **battle module**.
- **Video:**  

  https://github.com/user-attachments/assets/35c79819-b78b-4578-a4a2-af1235139807
</details>

<details>
  <summary>🔁 Auto Reload Module</summary>

Activate: `g_modules.enableAutoReload()` ([init.lua](https://github.com/mehah/otclient/blob/main/init.lua#L114))  
Video:  

https://github.com/kokekanon/otclient.readme/assets/114332266/0c382d93-6217-4efa-8f22-b51844801df4
</details>

<details>
  <summary>✨ Attached Effects System (aura, wings…)</summary>

- Compatible with **.APNG**
  - ThingCategoryEffect
  - ThingCategoryCreature
  - ThingExternalTexture: images in **PNG | APNG**
- **Wiki:** https://github.com/mehah/otclient/wiki/Tutorial-Attached-Effects
- **Example Code:** [effects.lua](https://github.com/mehah/otclient/blob/main/modules/game_attachedeffects/effects.lua) • [test code](https://github.com/mehah/otclient/blob/main/modules/game_attachedeffects/attachedeffects.lua#L1)  
- **Specific lookType settings:** [outfit_618.lua](https://github.com/mehah/otclient/blob/main/modules/game_attachedeffects/configs/outfit_618.lua)

> [!TIP]
> You can adjust offsets per looktype using **ThingConfig** when a default offset doesn’t align perfectly for a given sprite.

<p align="center">
<table>
<tr>
<td><img src="https://github.com/kokekanon/OTredemption-Picture-NODELETE/blob/main/Picture/Attached%20Effect/Creature/001_Bone.gif?raw=true" width="200"></td>
<td><img src="https://github.com/kokekanon/OTredemption-Picture-NODELETE/blob/main/Picture/Attached%20Effect/Creature/002_aura.gif?raw=true" width="200"></td>
<td><img src="https://github.com/kokekanon/OTredemption-Picture-NODELETE/blob/main/Picture/Attached%20Effect/Creature/003_particula.gif?raw=true" width="250"></td>
</tr>
<tr>
<td align="center">ThingCategory Attached Effect</td>
<td align="center">Texture (PNG) Attached Effect</td>
<td align="center">Particule</td>
</tr>
</table>
</p>
</details>
<details>
  <summary>🧭 Module Controller System</summary>

A safer way to create modules, without the need to unbind keys, disconnect events, or destroy widgets.  
**Example:** ([modules/game_minimap/minimap.lua](https://github.com/mehah/otclient/blob/cache-for-all/modules/game_minimap/minimap.lua))
</details>

<details>
  <summary>🖼️ Anti-Aliasing Mode Options</summary>

- *Note*: **Smooth Retro** will consume a little more GPU.

**GIF:**  
![aa](https://github.com/kokekanon/otclient.readme/assets/114332266/5a411525-7d5a-4b16-8bb6-2c6462152d39)
</details>

<details>
  <summary>🧩 Creature Information by UIWidget</summary>

- Enable: [setup.otml](https://github.com/mehah/otclient/blob/e2c5199e52bd86f573c9bb582d7548cfe7a8b026/data/setup.otml#L20)
- Style: [modules/game_creatureinformation](https://github.com/mehah/otclient/tree/main/modules/game_creatureinformation)
- **Note:** There is a performance degradation vs direct Draw Pool, about ~20%, tested with 60 monsters attacking each other.

**Video:**  

https://github.com/kokekanon/otclient.readme/assets/114332266/c2567f3f-136e-4e11-964f-3ade89c0056b
</details>

<details>
  <summary>🧱 Tile Widget</summary>

Wiki: https://github.com/mehah/otclient/wiki/Tutorial-Attached-Effects

<p align="center">
<table>
<tr>
<td><img src="https://github.com/kokekanon/OTredemption-Picture-NODELETE/blob/main/Picture/Attached%20Effect/Tile/001_attachedeffect.gif?raw=true" width="250"></td>
<td><img src="https://github.com/kokekanon/OTredemption-Picture-NODELETE/blob/main/Picture/Attached%20Effect/Tile/002_widget.png?raw=true" width="200"></td>
<td><img src="https://github.com/kokekanon/OTredemption-Picture-NODELETE/raw/main/Picture/Attached%20Effect/Tile/003_particulas.gif?raw=true" width="310"></td>
</tr>
<tr>
<td align="center">Title Attached Effect</td>
<td align="center">Title Widget</td>
<td align="center">Title Particule</td>
</tr>
</table>
</p>
</details>

<details>
  <summary>🧩 Support HTML/CSS Syntax</summary>

https://github.com/user-attachments/assets/b16359d3-09a4-4181-bcb8-c76339b64b37

https://github.com/user-attachments/assets/d3844223-7e35-45da-a872-3141f1c5860a

https://github.com/user-attachments/assets/9f20814f-0aed-4b70-8852-334ac745ec11  

https://github.com/user-attachments/assets/3ac8473c-8e90-4639-b815-ef183c7e2adf

**Module examples:**  
- [Shader](https://github.com/mehah/otclient/tree/main/modules/game_shaders)  
- [Blessing](https://github.com/mehah/otclient/pull/825)
</details>

<details>
  <summary>🎥 Latency-adaptive camera</summary>

Basically the camera adapts to the server latency to always remain smooth and avoid stuttering while walking.  
If the ping gets high, the camera moves slower to keep up with the server's response time; if the ping drops, the camera moves faster. *(Depends on character speed.)*
</details>

<details>
  <summary>🧭 Support Negative Offset (.dat)</summary>

- Compatible with [ObjectBuilderV0.5.5](https://github.com/punkice3407/ObjectBuilder/releases/tag/v0.5.5)  
- Enable: `g_game.enableFeature(GameNegativeOffset)`

**Video:**  

https://github.com/kokekanon/otclient.readme/assets/114332266/16aaa78b-fc55-4c6e-ae63-7c4063c5b032
</details>

- Floor Shadowing  
- Highlight Mouse Target *(press **Shift** to select any object)*  
- Floor View Mode *(Normal, Fade, Locked, Always, Always with transparency)*  
- Floating Effects Option  
- Refactored Walk System  
- Support for more mouse buttons *(e.g., 4 and 5)*
- Support DirectX  
- Hud Scale

---

### 🔗 Compatibility & Protocols
- Client **7.6 ~ 12.85 ~ 12.92**, **13.00 ~ 15.22** support *(protobuf)*  
- Market rewritten (compatible with TFS and Canary)  
- Async Texture Loading *(engine-level feature)*  
- Supports sequenced packages and compression


---

## <a id="compiling"></a>🔨 Compiling
If you are interested in compiling this project, visit the **[Wiki](https://github.com/mehah/otclient/wiki)**.




## <a id="support-protocol"></a>💯 Support Protocol

| Protocol / version      | Description                    | Required Feature | Compatibility |
|-------------------------|--------------------------------|---|---|
| Gunzodus (15.11 ~ 15.22) | Gunz                           |  | ✅ |

---

## <a id="license"></a>©️ License
OTClient is made available under the **MIT License** — you are free to use it for commercial, non-commercial, closed or open projects.  
See: [MIT License](http://opensource.org/licenses/MIT)

---

## <a id="contributors"></a>❤️ Contributors
If you are interested in supporting the project, donate here:  
**[PayPal](https://www.paypal.com/donate/?business=CV9D5JF8E46LY&no_recurring=0&item_name=Thank+you+very+much+for+your+donation.&currency_code=BRL)**
