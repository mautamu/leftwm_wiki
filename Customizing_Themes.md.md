##Theme Customization for leftwm

# What are these `.liquid` files and how do they work

When getting into customizing the theme of leftwm one of the more obscure things might be the `template.liquid` and `sizes.liquid` files.
They can be understood as a translation helper for leftwm-state to render the state of workspaces and tags into the syntax of the statusbar (e.g. `polybar`) used by the theme. 

Basically leftwm-state returns a json data structure like this pseudo-code:
```
 ├ "window_title"   <window title as string>
 └ "workspaces"     <array of workspaces>
      ├ "h"           <workspace height as int>
      ├ "w"           <workspace width as int>
      ├ "x"           <x-position of top-left corner of workspace as int>
      ├ "y"           <y-position of top-left corner of workspace as int>
      ├ "layout"      <currently active layout as string>
      ├ "index"       <index as string>
      └ "tags"        <array of tags for this workspace>
          ├ "name"      <tag name as string>
          ├ "index"     <index as int>
          ├ "mine"      <boolean is true, when the tag is owned by the active display>
          ├ "visible"   <boolean is true, when the tag active or is visible on another display>
          ├ "focused"   <boolean is true, when the focused window is on this tag>
          └ "busy"      <boolean is true, when the tag is not empty/has at least one window>
```

Here is a raw output example of `leftwm-state -q` (manually added line breaks for readability)
```json
{
  "window_title":"fish /home/vuimuich/.config/leftwm/themes/current",
  "workspaces":
  [{
    "h":1440,
    "w":2560,
    "x":0,
    "y":0,
    "layout":"Monocle",
    "index":0,
    "tags":
      [{
        "name":"1",
        "index":0,
        "mine":true,
        "visible":true,
        "focused":true,
        "busy":true
      },
      {
        "name":"2",
        "index":1,
        "mine":false,
        "visible":false,
        "focused":false,
        "busy":true
      },
      {
        "name":"3",
        "index":2,
        "mine":false,
        "visible":false,
        "focused":false,
        "busy":true
      }]
  }]
}
```
And this is the output with a template applied `leftwm-state -w 0 -t template_dev.liquid -n -q` 
```json
%{c}
leftwm-state /home/vuimuich/.config/leftwm/themes/current


%{A1:$SCRIPTPATH/change_to_tag 0 0:}
%{F#FFFFFF}%{B#455A64}  1  %{B-}%{F-}
%{A}



%{A1:$SCRIPTPATH/change_to_tag 0 1:}
%{F#90A4AE}  2  %{F-}
%{A}



%{A1:$SCRIPTPATH/change_to_tag 0 2:}
%{F#90A4AE}  3  %{F-}
%{A}
```
*Note: `$SCRIPTPATH/change_to_tag` is supposed to be executed by polybar*

The other big part of the .liquid files is polybar formatting tags. They are described in gread detail [in the polybar wiki](https://github.com/polybar/polybar/wiki/Formatting#format-tags)
