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


# keybind 