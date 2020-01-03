## Configuring LeftWM 

### All code snip-its in this section refer to the file `~/.config/leftwm/config.toml`


# Modkey
The modkey is the most import setting. It is used by many other settings and controls how key bindings work. 
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
All other commands are keybindings. you can think of key bindings as a way of telling LeftWM to do something when a key combination is pressed. There are several types of key bindings. In order for the keybind event to fire, the keys listed in the modifier section should be held down, and the key in the key section should then be pressed. Here is a [list](https://github.com/leftwm/leftwm/blob/master/src/utils/xkeysym_lookup.rs) of all keys LeftWM can use as a modifier or a key. 

Example
```
[[keybind]]
command = "Execute"
value = "vlc https://www.youtube.com/watch?v=oHg5SJYRHA0"
modifier = []
key = "XF86XK_AudioPlay"
```


# Keybind Commands
## Execute
## CloseWindow
## SoftReload
## MoveToLastWorkspace
## SwapTags
## MoveWindowUp
## MoveWindowDown
## FocusWindowUp
## FocusWindowDown
## NextLayout
## PreviousLayout
## FocusWorkspaceNext
## FocusWorkspacePrevious
## GotoTag
## MoveToTag

