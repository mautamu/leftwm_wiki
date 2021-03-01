# Configuring LeftWM

 _All code snippets in this section refer to the file `~/.config/leftwm/config.toml`_  
 All entries require a modifier, even if blank: `modifier = []`

## Terms

- _Default_ refers to the original `config.toml` specified when LeftWM first runs.  
- _Partial Default_ refers to a command that is in the original `config.toml` but is not the only instance.  
- _Example_ refers to a snippet that is not in the original `config.toml` but can be added or modified for additional features.

# Table of contents

- [Configuring LeftWM](#configuring-leftwm)
- [Modkey](#modkey)
- [Tags](#tags)
- [Workspaces](#workspaces)
- [Keybind](#keybind)
- [Keybind Commands](#keybind-commands)
  - [Execute](#execute)
  - [HardReload](#hardreload)
  - [SoftReload](#softreload)
  - [CloseWindow](#closewindow)
  - [MoveToLastWorkspace](#movetolastworkspace)
  - [MoveWindowUp](#movewindowup)
  - [MoveWindowDown](#movewindowdown)
  - [MoveWindowTop](#movewindowtop)
  - [MoveToTag](#movetotag)
  - [FocusWindowUp](#focuswindowup)
  - [FocusWindowDown](#focuswindowdown)
  - [NextLayout](#nextlayout)
  - [PreviousLayout](#previouslayout)
  - [FocusWorkspaceNext](#focusworkspacenext)
  - [FocusWorkspacePrevious](#focusworkspaceprevious)
  - [GotoTag](#gototag)
  - [FocusNextTag](#focusnexttag)
  - [FocusPreviousTag](#focusprevioustag)
  - [SwapTags](#swaptags)
  - [IncreaseMainWidth](#increasemainwidth)
  - [DecreaseMainWidth](#decreasemainwidth)
- [Troubleshooting](#troubleshooting)

# Modkey

The modkey is the most important setting. It is used by many other settings and controls how key bindings work.
For more info please read [this](https://stackoverflow.com/questions/19376338/xcb-keyboard-button-masks-meaning) post on x11 Mod keys

Default: `modkey = "Mod4"`  (windows key)

Example: `modkey = "Mod1"`  

# Tags

Tags are the names of the virtual desktops were windows live. In other window managers these are sometimes just called desktops. You can rename them to any unicode string including symbols/icons from popular icon libraries such as font-awesome.

Default: `tags = ["1", "2", "3", "4", "5", "6", "7", "8", "9"]`

Example: `tags = ["Browser ♖", "Term ♗", "Shell ♔", "Code ♕"]`

# Workspaces

Workspaces are how you view tags (desktops). A workspace is a area on a screen or most likely the whole screen. in this areas you can view a given tag.

Default: `workspaces = []` (one workspace per screen)

Example (two workspaces on a single ultrawide):

```toml
[[workspaces]]
y = 0
x = 0
height = 1440
width = 1720

[[workspaces]]
y = 0
x = 1720
height = 1440
width = 1720
```

# Keybind

All other commands are keybindings. you can think of key bindings as a way of telling LeftWM to do something when a key combination is pressed. There are several types of key bindings. In order for the keybind event to fire, the keys listed in the modifier section should be held down, and the key in the key section should then be pressed. [Here is a list of all keys LeftWM can use as a modifier or a key](https://github.com/leftwm/leftwm/blob/master/src/utils/xkeysym_lookup.rs).

Example:

```toml
[[keybind]]
command = "Execute"
value = "vlc https://www.youtube.com/watch?v=oHg5SJYRHA0"
modifier = []
key = "XF86XK_AudioPlay"
```

**Note: even if blank, a modifier must be present! Use `modifier= []` for no modifier**

# Keybind Commands

## Execute

Execute a shell command when a key combination is pressed.

Partial default:

```toml
[[keybind]]
command = "Execute"
value = "rofi -show run"
modifier = ["modkey"]
key = "p"
```

**Note: This command requires a value field to be specified**.

## HardReload

Completely restarts LeftWM.

Example:

```toml
[[keybind]]
command = "SoftReload"
modifier = ["modkey", "Shift"]
key = "b"
```

## SoftReload

Restarts LeftWM but remembers the state of all windows. This is useful when playing with the config file or themes.

Default:

```toml
[[keybind]]
command = "SoftReload"
modifier = ["modkey", "Shift"]
key = "r"
```

## CloseWindow

Closes the window that is currently focused. This is not a forceful quit. It is equivalent to clicking the (x) in the top right of a window normally.

Default:

```toml
[[keybind]]
command = "CloseWindow"
modifier = ["modkey", "Shift"]
key = "q"
```

## MoveToLastWorkspace

Takes the window that is currently focused and moves it to the workspace that was active before the current workspace.

Default:

```toml
[[keybind]]
command = "MoveToLastWorkspace"
modifier = ["modkey", "Shift"]
key = "w"
```

## MoveWindowUp

Re-orders the focused window within the current workspace (moves up in order).

Default:

```toml
[[keybind]]
command = "MoveWindowUp"
modifier = ["modkey", "Shift"]
key = "Up"
```

## MoveWindowDown

Re-orders the focused window within the current workspace (moves down in order).

Default:

```toml
[[keybind]]
command = "MoveWindowDown"
modifier = ["modkey", "Shift"]
key = "Down"
```

## MoveWindowTop

Re-orders the focused window within the current workspace (moves to the top of the stack).

Default:

```toml
[[keybind]]
command = "MoveWindowTop"
modifier = ["modkey"]
key = "Return"
```

## MoveToTag

Moves a window to a given tag.

Partial default:

```toml
[[keybind]]
command = "MoveToTag"
value = "1"
modifier = ["modkey", "Shift"]
key = "1"
```

**Note: This command requires a value field to be specified**.

## FocusWindowUp

Focuses the window that is one higher in order on the current workspace.

Default:

```toml
[[keybind]]
command = "FocusWindowUp"
modifier = ["modkey"]
key = "Up"
```

## FocusWindowDown

Focuses the window that is one lower in order on the current workspace.

Default:

```toml
[[keybind]]
command = "FocusWindowDown"
modifier = ["modkey"]
key = "Down"
```

## NextLayout

Changes the workspace to a new layout.

Default:

```toml
[[keybind]]
command = "NextLayout"
modifier = ["modkey", "Control"]
key = "Up"
```

## PreviousLayout

Changes the workspace to the previous layout.

Default:

```toml
[[keybind]]
command = "PreviousLayout"
modifier = ["modkey", "Control"]
key = "Down"
```

## FocusWorkspaceNext

Moves the focus from the current workspace to the next workspace (next screen).

Default:

```toml
[[keybind]]
command = "FocusWorkspaceNext"
modifier = ["modkey"]
key = "Right"
```

## FocusWorkspacePrevious

Moves the focus from the current workspace to the previous workspace (previous screen).

Default:

```toml
[[keybind]]
command = "FocusWorkspacePrevious"
modifier = ["modkey"]
key = "Left"
```

## GotoTag

Changes the tag that is being displayed in a given workspace.

Partial default:

```toml
[[keybind]]
command = "GotoTag"
value = "9"
modifier = ["modkey"]
key = "9"
```

**Note: This command requires a value field to be specified**.

## FocusNextTag

Moves the focus from the current tag to the next tag in a given workspace.

Example:

```toml
[[keybind]]
command = "FocusNextTag"
modifier = ["modkey"]
key = "Right"
```

## FocusPreviousTag

Moves the focus from the current tag to the previous tag in a given workspace.

Example:

```toml
[[keybind]]
command = "FocusPreviousTag"
modifier = ["modkey"]
key = "Left"
```

## SwapTags

Swaps the tags in the current workspace with the tags in the previous workspace.

Default:

```toml
[[keybind]]
command = "SwapTags"
modifier = ["modkey"]
key = "w"
```

## IncreaseMainWidth

Increases the width of the currently focused window.

Example:

```toml
[[keybind]]
command = "IncreaseMainWidth"
value = "5"
modifier = ["modkey"]
key = "a"
```

**Note: This command requires a value field to be specified**.

## DecreaseMainWidth

Decreases the width of the currently focused window.

Example:

```toml
[[keybind]]
command = "DecreaseMainWidth"
value = "5"
modifier = ["modkey"]
key = "x"
```

**Note: This command requires a value field to be specified**.

## Troubleshooting

| Issue | Description | Solution |
|-|-|:-:|
| No config.toml file exists | LeftWM does not always ship with a `config.toml`. You will need to execute LeftWM at least once for one to be generated. | Try the following: ``` leftwm-worker ``` |
| Config.toml is not being parsed | LeftWM ships with a binary called leftwm-check. It might not be installed by the AUR. | Try the following: ``` leftwm-check ``` |
| Keybinding doesn't work/foreign keyboards | You may need to set the modifier (`modifier = []`) or to specify the name of the key, e.g. `eacute` for é. If it is a keypad number, use a modkey with value `lock`.| Refer to [this](https://github.com/leftwm/leftwm/blob/master/src/utils/xkeysym_lookup.rs) list of keys |
| Keybinding doesn't work | It's likely you need to specify a value, a modifier, or have a typo. | Refer to the definition above or open an issue |
