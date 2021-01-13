## Configuring LeftWM 

### All code snip-its in this section refer to the file `~/.config/leftwm/config.toml`


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

Example (two workspaces on a single ultrawide ): 

```
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

*Example*
```
[[keybind]]
command = "Execute"
value = "vlc https://www.youtube.com/watch?v=oHg5SJYRHA0"
modifier = []
key = "XF86XK_AudioPlay"
```


# Keybind Commands

## Execute
Execute a shell command when a key combination is pressed.

Example
```
[[keybind]]
command = "Execute"
value = "rofi -show run"
modifier = ["modkey"]
key = "p"
```

## HardReload
Completely restarts LeftWM. 

## SoftReload
Restarts LeftWM but remembers the state of all windows. This is useful when playing with the config file.

## CloseWindow
Closes the window that is currently focused. This is not a forceful quit. It is equivalent to clicking the (x) in the top right of a window normally. 

## MoveToLastWorkspace
Takes the window that is currently focused and moves it to the workspace that was active before the current workspace.

## MoveWindowUp
Re-orders the focused window within the current workspace (moves up in order).

## MoveWindowDown
Re-orders the focused window within the current workspace (moves down in order).

## MoveWindowTop
Re-orders the focused window within the current workspace (moves to the top of the stack).

## MoveToTag
Moves a window to a given tag.

## FocusWindowUp
Focuses the window that is one higher in order on the current workspace.

## FocusWindowDown
Focuses the window that is one lower in order on the current workspace.

## NextLayout
Changes the workspace to a new layout.

## PreviousLayout
Changes the workspace to the previous layout.

## FocusWorkspaceNext
Moves the focus from the current workspace to the next workspace (next screen).

## FocusWorkspacePrevious
Moves the focus from the current workspace to the previous workspace (previous screen).

## GotoTag
Changes the tag that is being displayed in a given workspace.

## FocusNextTag
Moves the focus from the current tag to the next tag in a given workspace.

## FocusPreviousTag
Moves the focus from the current tag to the previous tag in a given workspace.

## SwapTags
Swaps the tags in the current workspace with the tags in the previous workspace.

## IncreaseMainWidth
Increases the width of the currently focused window.

## DecreaseMainWidth
Decreases the width of the currently focused window.
