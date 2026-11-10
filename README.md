<div align="center">

# 🌑 Darksoul UI Library

### A sleek, themeable Roblox UI library with a Redz-style API

![Version](https://img.shields.io/badge/version-2.0.0-8B5CF6?style=for-the-badge)
![Language](https://img.shields.io/badge/Lua-Roblox-2C2D72?style=for-the-badge&logo=lua&logoColor=white)
![Platform](https://img.shields.io/badge/PC%20%2B%20Mobile-supported-34D399?style=for-the-badge)
![Themes](https://img.shields.io/badge/themes-11-C084FC?style=for-the-badge)
[![Discord](https://img.shields.io/badge/Discord-Join%20us-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/vuGAKj8t22)

[**Getting Started**](#-getting-started) •
[**Window**](#-window) •
[**Options**](#-options) •
[**Key System**](#-key-system) •
[**Themes**](#-themes) •
[**Example**](#-full-example)

*Made by **Demon** • Discord: `greensoul8410`*

</div>

---

## ✨ Why Darksoul UI?

Darksoul UI keeps the familiar `MakeWindow` / `MakeTab` / `AddToggle` API, so scripts written for Redz or Wand UI are easy to port, and adds a lot on top.

| | | |
|---|---|---|
| 🎨 **11 themes** + custom themes and accent color | 🔍 **Built-in search** | ⌨️ **Keybinds** (also on toggles) |
| 🖌️ **Color picker** | 🔔 **Notifications & dialogs** | 🔑 **Key system** with tiers and locks |
| 💾 **Auto-saved flags** and named profiles | 🧩 **Groups** (two columns) | 🔗 **Option dependencies** |
| 🌌 **Backgrounds & backdrop effects** | ⚙️ **Built-in Settings tab** | 📱 **PC + mobile support** |

---

## 📑 Table of Contents

1. [Getting Started](#-getting-started)
2. [Window](#-window)
3. [Tabs, Dialogs & Notifications](#-tabs-dialogs--notifications)
4. [Options](#-options)
5. [Dependencies, Locks & Tooltips](#-dependencies-locks--tooltips)
6. [Key System](#-key-system)
7. [Credits](#-credits)
8. [Themes](#-themes)
9. [UI Scale](#-ui-scale)
10. [Flags & Profiles](#-flags--profiles)
11. [Settings Tab](#-built-in-settings-tab)
12. [Full Example](#-full-example)
13. [Notes & License](#-notes)

---

## 🚀 Getting Started

Load the library with one line:

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/darksoulhubcode/DarksoulHub/refs/heads/main/DarksoulUILibrary"))()
```

> 💡 Re-running the script destroys the previous UI automatically, so you never get duplicates.

### Create a Window

```lua
local Window = Library:MakeWindow({
  Title = "Darksoul Hub : Cool Game",
  SubTitle = "dev by Demon",
  ScriptFolder = "DarksoulHub"
})
```

`Library:CreateWindow` is an alias of `MakeWindow`. A compact form also works:

```lua
local Window = Library:MakeWindow({ "Title", "SubTitle", "Folder" })
```

<details>
<summary><b>⚙️ Window config options</b></summary>

<br>

| Key | Type | Description |
|---|---|---|
| `Title` / `Name` | string | Window title |
| `SubTitle` | string | Text under the title |
| `ScriptFolder` / `FolderName` | string | Folder used to save flags and profiles (default `DarksoulHub`) |
| `Theme` | string | Starting theme (default `Violet`) |
| `Size` | `UDim2` / `Vector2` | Window size in pixels (default 640 x 390) |
| `Icon` | string | Window icon |
| `MenuKey` | `Enum.KeyCode` | Key that shows or hides the UI (default `LeftControl`) |
| `Density` | string | `Compact`, `Default` or `Comfortable` |
| `Font` | string | `Gotham`, `Montserrat`, `SourceSans`, `Ubuntu`, `Nunito` or `Fredoka` |
| `Sidebar` | string | `Full` or `Compact` |
| `UITransparency` | number | Panel transparency (0 to 0.9) |
| `Background` | string | Preset name, asset id, URL or file path |
| `BackgroundTransparency` | number | Background image transparency |
| `Effect` | string | `None`, `Snow`, `Sakura`, `Fireflies`, `Embers`, `Matrix` or `Rain` |
| `Credits` | table | Team list, see [Credits](#-credits) |
| `Social` | table | Community links, see [Credits](#-credits) |
| `Key` | table or `true` | Key system, see [Key System](#-key-system) |

</details>

---

## 🪟 Window

### Window API

| Method | Description |
|---|---|
| `NewMinimizer({ KeyCode })` → `Minimizer` | Create a minimizer bound to a key |
| `MakeTab({ Title, Icon })` → `Tab` | Create a tab |
| `SelectTab(Tab \| number)` | Select a tab |
| `SetVisible(boolean)` / `Toggle()` | Show, hide or toggle the window |
| `Notify(config)` → `Notification` | Show a notification |
| `NewNotifyGroup(config)` → `NotificationGroup` | Create a notification group |
| `Dialog({ Title, Content, Options })` → `Dialog` | Show a dialog |
| `SetUIScale(number)` | Change the UI scale |
| `SetTitle(string)` / `SetSubTitle(string)` | Change title or subtitle |
| `GetTitle()` / `GetSubTitle()` | Read title or subtitle |
| `SetTransparency(number)` | Panel transparency |
| `SetBackground(spec, imageAlpha?)` | Set the background (`nil` clears it) |
| `SetEffect(name)` | Backdrop effect |
| `SetDensity(name)` | `Compact`, `Default` or `Comfortable` |
| `SetSidebar("Full" \| "Compact")` | Sidebar mode |
| `ShowCredits()` | Open the credits popup |
| `GetFlag(flag)` / `SetFlag(flag, value)` | Read or write a saved value |
| `DeleteFlags()` | Delete every saved value |
| `SaveConfig(name)` / `LoadConfig(name)` / `DeleteConfig(name)` | Manage profiles |
| `ListConfigs()` | List saved profiles |
| `ResetToDefaults()` | Reset every option to its default |
| `Destroy()` | Remove the window |

### Minimizer

```lua
local Minimizer = Window:NewMinimizer({
  KeyCode = Enum.KeyCode.LeftControl
})

local MobileButton = Minimizer:CreateMobileMinimizer({
  Image = "rbxassetid://0",
  BackgroundColor3 = Color3.fromRGB(0, 0, 0)
})
```

| Member | Description |
|---|---|
| `Minimize()` | Hide the window |
| `Cancel()` | Show the window again |
| `CreateMobileMinimizer(props)` → `ImageButton` | Create the mobile button |
| `Window.IsMinimied` | `boolean` |

---

## 🗂️ Tabs, Dialogs & Notifications

### Creating a Tab

```lua
-- Normal
local Tab = Window:MakeTab({
  Title = "Cool Tab",
  Icon = "Home"
})

-- Compact
local Tab = Window:MakeTab({ "Cool Tab", "Home" })
```

| Member | Description |
|---|---|
| `Select()` | Select this tab |
| `SetVisible(boolean)` | Show or hide the tab |
| `SetLocked(boolean \| string)` | Lock the tab behind a key or tier |
| `Destroy()` | Remove the tab |
| `Title`, `Icon` | Tab properties |

### Creating a Dialog

```lua
Window:Dialog({
  Title = "Hello!",
  Content = "do you like Coffee?",
  Options = {
    {
      Name = "No"
    },
    {
      Name = "Yes!",
      Callback = function(self)
        print("Yes, i like Coffee")
      end
    }
  }
})
```

| Member | Description |
|---|---|
| `Close()` | Close the dialog |
| `NewOption({ Name, Callback? })` | Add another button |

### Creating a Notification

```lua
Window:Notify({
  Title = "Notification",
  Content = "this is a Notification",
  Type = "Success",
  Duration = 5
})
```

`Library:Notify` works too, without needing a window.

| Key | Type | Description |
|---|---|---|
| `Title` | string | Notification title |
| `Content` | string | Notification text |
| `Type` | string | `Info` (default), `Success`, `Warning` or `Error` |
| `Image` / `Icon` | string | Custom icon, overrides the type icon |
| `Duration` | number | Seconds on screen (default 5) |
| `Id` | string | Replaces any existing notification with the same id |
| `Buttons` | table | `{ { Text = "Click", Callback = function() end } }` |

A notification has `Close()` and `Closed`. Change where they appear with `Library:SetNotifyPosition("BottomRight")` (`BottomRight`, `TopRight`, `BottomLeft`, `TopLeft`).

---

## 🧩 Options

### Everything you can add

| Function | What it creates |
|---|---|
| `AddSection(title)` | Section header (can be collapsible) |
| `AddDivider()` | A divider line |
| `AddParagraph(title, description)` | Text block |
| `AddGroup({ Name, Side })` | Left / right column group |
| `AddToggle` | On / off switch |
| `AddButton` | Button |
| `AddSlider` | Slider |
| `AddRangeSlider` | Slider with two handles |
| `AddStepper` | + / − number input |
| `AddDropdown` | Dropdown (single or multi select) |
| `AddTextBox` | Text input |
| `AddKeybind` | Keybind picker |
| `AddColorPicker` | Color picker |
| `AddProgress` | Progress bar |
| `AddStatus` | Status label (can auto-update) |
| `AddImage` | Image card |
| `AddDiscordInvite` | Discord invite card |

### Shared builder

Every option accepts these keys:

| Key | Description |
|---|---|
| `Name` / `Title` | Option title |
| `Desc` / `Description` | Small text under the title |
| `Tooltip` | Hover tooltip |
| `Flag` | Saves the value automatically |
| `Locked` | `true` or a tier name, see [Key System](#-key-system) |
| `DependsOn` / `DependsMode` | Show or disable depending on another option |

### Shared functions

| Function | Description |
|---|---|
| `SetTitle(text)` / `SetDescription(text)` | Change the text |
| `SetVisible(boolean)` | Show or hide |
| `SetTooltip(text)` | Change the tooltip |
| `SetLocked(boolean \| string)` / `IsLocked()` | Lock control |
| `SetDisabled(boolean)` | Grey out the option |
| `SetDependsOn(rule, mode?)` | Add a dependency |
| `AddCallback(function)` | Add another callback |
| `Destroy()` | Remove the option |
| `Title`, `Description`, `Kind` | Properties |

### Per-option members

| Option | Members |
|---|---|
| **Toggle** | `Value`, `SetValue(bool)`, `Get()` |
| **Slider** | `Value`, `Min`, `Max`, `Increment`, `SetValue(n)`, `Get()` |
| **RangeSlider** | `Value = { Min, Max }`, `SetValue(min, max)` |
| **Dropdown** | `Value`, `SetValue`, `GetSelected()`, `Add(...)`, `Remove(option)`, `NewOptions({...})`, `Clear()`, `GetOptionsCount()` |
| **TextBox** | `Value`, `SetText`, `GetText`, `CaptureFocus`, `SetTextFilter(fn)`, `SetPlaceholder`, `Clear` |
| **Keybind** | `Value` (`EnumItem`), `SetValue(key)` |
| **ColorPicker** | `Value` (`Color3`), `SetValue(color)` |
| **Status** | `Value`, `SetValue(text, tone)` with tone `Success`, `Warning` or `Error` |
| **Button** | `Fire()` |
| **Section** | `SetCollapsed(state)`, `Destroy()` |
| **Group** | `SetTitle`, `SetCollapsed`, `SetVisible`, `SetLocked`, `Select`, `Destroy` |

> Options can also be created directly on a group: `Group:AddToggle({ ... })`.

### Examples

<details open>
<summary><b>📌 Section & Paragraph</b></summary>

```lua
Tab:AddSection("Section")

-- Collapsible
Tab:AddSection({ Title = "Section", Collapsible = true, Collapsed = false })

Tab:AddParagraph("Paragraph", "This is a Paragraph\nSecond Line")
```

</details>

<details open>
<summary><b>🔘 Toggle</b></summary>

```lua
Tab:AddToggle({
  Name = "Toggle",
  Default = false,
  Callback = function(Value)

  end
})
```

**Toggle keybind & extra panel.** A toggle can have its own keybind chip and a settings gear:

```lua
local Toggle = Tab:AddToggle({ Name = "Auto Farm", Flag = "autofarm" })

Toggle:AddKeybind({
  Default = Enum.KeyCode.F,
  Mode = "Toggle" -- "Toggle", "Hold" or "Always"
})

local Extra = Toggle:Extra() -- opens a gear panel you can fill with options
```

</details>

<details open>
<summary><b>🖱️ Button</b></summary>

```lua
Tab:AddButton({
  Name = "My Button",
  Debounce = 0.5,
  Callback = function()

  end
})
```

</details>

<details open>
<summary><b>🎚️ Slider, Range Slider & Stepper</b></summary>

```lua
Tab:AddSlider({
  Name = "Cool Title",
  Min = -5,
  Max = 5,
  Increment = 0.25,
  Default = 0,
  Callback = function(Value)

  end
})

Tab:AddRangeSlider({
  Name = "Distance",
  Min = 0,
  Max = 100,
  DefaultMin = 20,
  DefaultMax = 80,
  MinGap = 5,
  Callback = function(MinValue, MaxValue)

  end
})

Tab:AddStepper({
  Name = "Amount",
  Min = 1,
  Max = 10,
  Increment = 1,
  Default = 1,
  Callback = function(Value)

  end
})
```

</details>

<details open>
<summary><b>📋 Dropdown</b></summary>

```lua
Tab:AddDropdown({
  Name = "Dropdown",
  Options = {"one", "two", "three", "four", "five"},
  Default = "one",
  Callback = function(Value)

  end
})

-- Multi select
Tab:AddDropdown({
  Name = "Dropdown",
  MultiSelect = true,
  Options = {"one", "two", "three", "four", "five"},
  Default = {"one", "four"},
  Callback = function(Value)

  end
})
```

</details>

<details open>
<summary><b>⌨️ TextBox, Keybind & Color Picker</b></summary>

```lua
Tab:AddTextBox({
  Name = "My TextBox",
  Default = "text",
  Placeholder = "input text...",
  ClearOnFocus = true,
  Numeric = false,
  Callback = function(Value)

  end
})

Tab:AddKeybind({
  Name = "Menu Key",
  Default = Enum.KeyCode.RightShift,
  Changed = function(Key)

  end
})

Tab:AddColorPicker({
  Name = "ESP Color",
  Default = Color3.fromRGB(255, 0, 0),
  Callback = function(Color)

  end
})
```

</details>

<details open>
<summary><b>📊 Progress, Status & Image</b></summary>

```lua
Tab:AddProgress({ Name = "Progress", Min = 0, Max = 100, Default = 50, Suffix = "%" })

local Status = Tab:AddStatus({ Name = "Status", Value = "Idle", Tone = "Warning" })
Status:SetValue("Running", "Success")

-- Auto-updating status
Tab:AddStatus({
  Name = "FPS",
  UpdateRate = 1,
  Update = function()
    return "60"
  end
})

Tab:AddImage({
  Image = "rbxassetid://0",
  Caption = "My Image",
  Height = 110
})
```

</details>

<details open>
<summary><b>🧱 Group (two columns)</b></summary>

```lua
local Left = Tab:AddGroup({ Name = "Farming", Side = "Left" })
local Right = Tab:AddGroup({ Name = "Misc", Side = "Right" })

Left:AddToggle({ Name = "Auto Farm" })
Right:AddButton({ Name = "Rejoin", Callback = function() end })
```

Groups also accept `Collapsible`, `Collapsed` and `Locked`.

</details>

<details open>
<summary><b>💬 Discord Invite card</b></summary>

```lua
MainTab:AddDiscordInvite({
  Title = "Darksoul Hub | Community",
  Description = "Official scripts, updates and support in one place.",
  Banner = "rbxassetid://0", -- You can put an RGB Color: Color3.fromRGB(233, 37, 69)
  Logo = "rbxassetid://0",
  Invite = "https://discord.gg/vuGAKj8t22",
  Members = 1000, -- Optional
  Online = 100, -- Optional
})
```

</details>

---

## 🔗 Dependencies, Locks & Tooltips

Show, hide or disable an option depending on another option's flag:

```lua
Tab:AddToggle({ Name = "Advanced", Flag = "advanced" })

Tab:AddSlider({
  Name = "Advanced Speed",
  Min = 1, Max = 10,
  DependsOn = "advanced",   -- flag name
  DependsMode = "Disable",  -- "Hide" (default) or "Disable"
  Tooltip = "Only works when Advanced is on."
})
```

`DependsOn` accepts:

| Rule | Meaning |
|---|---|
| `"flag_name"` | The option with that flag is on / not empty |
| `function() return bool end` | Any custom check |
| `{ Flag = "mode", Equals = "Fast" }` | The flag equals a value |
| `{ Flag = "advanced", Not = true }` | The flag is off / empty |

---

## 🔑 Key System

Enable a key system by passing `Key` to `MakeWindow`:

```lua
local Window = Library:MakeWindow({
  Title = "Darksoul Hub",
  Key = {
    Prompt = true,    -- open the key prompt on start
    Full = false,     -- lock the entire window until a key is valid
    Remember = true,  -- save a valid key (default true)
    Validate = function(key)
      -- return true (or true, "Premium") when the key is valid
      -- return false, "reason" when it is not
      return key == "my-key", "Premium"
    end
  }
})
```

Lock an option or a tab behind a key or a tier:

```lua
Tab:AddToggle({ Name = "Premium Feature", Locked = "Premium" })
Tab:AddButton({ Name = "Any Valid Key", Locked = true, Callback = function() end })
```

| Method | Description |
|---|---|
| `SetKeyValidator(fn, config?)` | Set the validator after creating the window |
| `CheckKey(key)` → `Success, Info?` | Validate a key |
| `KeyPrompt()` | Open the key prompt |
| `ClearKey()` | Remove the saved key |
| `IsUnlocked()` | `true` if a valid key is set |
| `GetTier()` | The tier returned by `Validate` |
| `OnAccessChanged(fn)` | Called when access changes |

<details>
<summary><b>🔧 All Key config fields</b></summary>

<br>

| Key | Description |
|---|---|
| `Prompt` | Open the key prompt on start |
| `Full` | Lock the entire window until a valid key is entered |
| `Remember` | Save a valid key (default `true`) |
| `Validate` | `function(key)` returning `valid, tier` |
| `Title` / `Note` | Text shown on the key prompt |
| `Link` | "Get key" link, copied to the clipboard when pressed |
| `OnGetKey` | Function called with `Link` when the get-key button is pressed |
| `AllowFree` | When `Full = true`, shows a **Continue Freemium** button (default `true`, set `false` to hide it) |
| `LockTitle` / `LockNote` | Text shown on locked options |

The tier returned by `Validate` (second return value) is shown next to the subtitle. `Freemium`, `Premium` and `Developer` have their own colors. A `Developer` tier unlocks everything.

</details>

---

## 🏷️ Credits

```lua
local Window = Library:MakeWindow({
  Title = "Darksoul Hub",
  Credits = {
    { Name = "Demon", Role = "ServerOwner", Url = "https://discord.com/users/0" }
  },
  Social = {
    { Label = "Discord", SubLabel = "discord.gg/vuGAKj8t22", CopyText = "https://discord.gg/vuGAKj8t22" }
  }
})
```

Built-in role colors: `ServerOwner`, `MainDeveloper`, `WebDesigner`, `Tester`, `Support`. A **Credits** button appears in Settings when either table is provided.

---

## 🎨 Themes

11 built-in themes (default: `Violet`):

![Purple](https://img.shields.io/badge/Purple-C084FC?style=flat-square)
![Crimson](https://img.shields.io/badge/Crimson-FC6484?style=flat-square)
![Ocean](https://img.shields.io/badge/Ocean-50C8F0?style=flat-square)
![Emerald](https://img.shields.io/badge/Emerald-50DC82?style=flat-square)
![Sunset](https://img.shields.io/badge/Sunset-FCB450?style=flat-square)
![Rose](https://img.shields.io/badge/Rose-FA82B9?style=flat-square)
![Midnight](https://img.shields.io/badge/Midnight-788CFA?style=flat-square)
![Toxic](https://img.shields.io/badge/Toxic-BEF03C?style=flat-square)
![Silver](https://img.shields.io/badge/Silver-C8CBD7?style=flat-square)
![Violet](https://img.shields.io/badge/Violet-C878FA?style=flat-square)
![Halloween](https://img.shields.io/badge/Halloween-FF8214?style=flat-square)

| Function | Description |
|---|---|
| `Library:SetTheme(name)` | Switch theme |
| `Library:GetTheme(name?)` | Get a theme table |
| `Library:GetThemes()` | List theme names |
| `Library:IsValidTheme(name)` | Check a theme exists |
| `Library:AddTheme(name, definition)` | Add your own theme |
| `Library:SetAccent(color?)` | Override the accent color (`nil` resets it) |
| `Library:SetFont(name)` | Change the font |
| `Library:GetIconByName(name)` | Get an icon asset by name |

**Custom theme**

```lua
Library:AddTheme("Blood", {
  Body = Color3.fromRGB(12, 6, 6),
  Accent = Color3.fromRGB(255, 40, 60),
  -- optional: Primary, AccentDark, AccentLight, Header, Text, SubText, Lit, ButtonGradient
})
Library:SetTheme("Blood")
```

Only `Accent` and `Body` are really needed, everything else is derived from them.

---

## 📐 UI Scale

| | |
|---|---|
| Min Scale | `0.6` |
| Max Scale | `1.6` |
| Default Scale | `1.0` |

```lua
Library:SetUIScale(1.0)
print(`UI Min Scale is: {Library:GetMinScale()} and the maximum is: {Library:GetMaxScale()}`)
```

---

## 💾 Flags & Profiles

Give an option a `Flag` and its value is saved automatically to `<ScriptFolder>/Flags.json` and restored on the next run (requires executor file access).

```lua
Tab:AddToggle({
  Name = "Cool Toggle",
  Flag = "toggle_flag"
})

local ToggleValue = Window:GetFlag("toggle_flag") or false

-- Manual flags
Window:SetFlag("my_custom_flag", 123)
```

Named profiles can be saved and loaded from the Settings tab, or from code:

```lua
Window:SaveConfig("legit")
Window:LoadConfig("legit")
print(Window:ListConfigs())
Window:DeleteConfig("legit")
Window:ResetToDefaults()
```

---

## ⚙️ Built-in Settings Tab

Every window gets a pinned **Settings** tab with:

> theme • accent color • UI scale • UI transparency • density • font • sidebar mode • menu key • notification position • tooltips • background presets and custom image • backdrop effects • profiles • credits • reset saved settings • unload UI

Background presets: `Aurora`, `Deep Violet`, `Ember`, `Forest`, `Midnight`, `Mono`, `Ocean`, `Rose`. Custom backgrounds accept asset ids everywhere; URLs and files need `getcustomasset` support in your executor.

---

## 🧪 Full Example

```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/darksoulhubcode/DarksoulHub/refs/heads/main/DarksoulUILibrary"))()

local Window = Library:MakeWindow({
  Title = "Darksoul Hub : Cool Game",
  SubTitle = "dev by Demon",
  ScriptFolder = "DarksoulHub"
})

local Minimizer = Window:NewMinimizer({ KeyCode = Enum.KeyCode.LeftControl })
Minimizer:CreateMobileMinimizer({ Image = "rbxassetid://0" })

local Main = Window:MakeTab({ "Main", "Home" })

Main:AddSection("Farming")

Main:AddToggle({
  Name = "Auto Farm",
  Flag = "autofarm",
  Callback = function(Value)
    print("Auto Farm:", Value)
  end
})

Main:AddSlider({
  Name = "Walk Speed",
  Min = 16, Max = 100, Increment = 1, Default = 16,
  Callback = function(Value)
    local hum = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
    if hum then hum.WalkSpeed = Value end
  end
})

Main:AddButton({
  Name = "Say Hello",
  Callback = function()
    Window:Notify({ Title = "Hello", Content = "Darksoul UI works!", Type = "Success", Duration = 4 })
  end
})
```

### 🧹 Destroying the UI

```lua
Window:Destroy()   -- remove one window
Library:Destroy()  -- remove everything and disconnect all connections
```

---

## 📝 Notes

- File saving (flags, profiles, remembered keys) requires `isfile`, `readfile`, `writefile` and `makefolder`. Without them the UI still works, it just won't persist.
- Custom URL / file backgrounds require `getcustomasset`.
- Fonts, density, accent, menu key and other cosmetic settings are saved per `ScriptFolder`.

---

<div align="center">

## 📜 License

Copyright © 2026 **Demon** (`greensoul8410`). All rights reserved.

This library is proprietary and is for use in Darksoul Hub only. You may not copy, modify, redistribute, resell or reuse this code, in whole or in part, without written permission from the author. For permission, contact `greensoul8410` on Discord.

<br>

[![Discord](https://img.shields.io/badge/Join%20the%20Darksoul%20Hub%20Discord-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.gg/vuGAKj8t22)

*Made with 🖤 by Demon*

</div>
