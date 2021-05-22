# Theme Customization for leftwm with `liquid`

## What are these `.liquid` files and how do they work

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

Here is a raw output example of `leftwm-state -q` (manually added line breaks for readability, tags 4-9 omitted)
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

## Example use

We can use the `liquid` templating language with this structure to generate inline code for the configuration languages of status bars or shell scripts or provide any of the above with specific values.
In the following examples we will focus on `Polybar`, `Lemonbar` and `EWW` as these apear to be quite popular and resemble different approaches on handling templates. Other status bars like `xmobar`, `cnx`, `yuzubar` etc. should basically all work in a similar way.

There are two ways to use `liquid-syntax` with `leftwm-state`, inline literal strings or template files:
1. to use `leftwm-state` with the inline literal string you can use the `-s` command switch:
   ```sh
   leftwm-state -w 0 -s {{ worspace.layout }} # the switch '-w 0' tells leftwm-state to return values for workspace[0]
   ```
   This is typically most helpfull when you want to get only a single return value, like the current layout as in the example, or the name of a specific tag.similar, but some logic is possible as well.
2. but for bigger templates with a bunch of styling and logic a dedicated `.liquid` template file might be the better fit.
   To make use of this, use the command switch `-t`, like in the playbar example below.

*Note: Since all theme-related processes are child-processes of the `up` script they usually can use `$SCRIPTPATH` to set the path for theme-specific scripts.*

## Polybar

Let have a look at the output with a template applied with the command: `leftwm-state -w 0 -t <leftwm-config-dir>/basic_polybar/template_dev.liquid -n -q`
```polybar
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
*Note: `$SCRIPTPATH/change_to_tag` here is an inline literal to exectue the `change_to_tag` shell script when clicking on the tag in polybar*.

The other big part of the output is polybar formatting tags. They are described in gread detail [in the polybar wiki](https://github.com/polybar/polybar/wiki/Formatting#format-tags)

*Note: With polybar it can happen in a few situations that you will see an Error-Message instead of your tags.*
     *This usually happens when `leftwm-state` is slower then polybar durin gstartup, or fails to deliver proper output as result of a crashed `leftwm-worker`*
     *This is a known issue (#207 and #275).*


## EWW

*Note: Currently `EWW` is in the process of migrating away from `XML` as its config language, so please be aware that the following example is expeted to break in the future. Please keep track of their migration process on their (github)[https://github.com/elkowar/eww]. We will try to update this section as soon as reasonable.*

With `eww` we run the command/script from within their configuration file just as polybar does, but their configuration (at least as long as they are using `XML`) might have some pitfalls prepared for you. Therefore we will go into settng up a template for `eww` in a bit more detail.
We use the example bar of `eww` as shipped with their repository, so you'll find just a bunch of snippets to add to their `eww.xml`

This following is the complete `template.liquid` of the `baseic_eww` example theme: 
```liquid
{% assign mine_open = '<button class="ws-button-mine" onclick="wmctrl -s ' %}
{% assign visible_open = '<button class="ws-button-visible" onclick="wmctrl -s ' %}
{% assign busy_open = '<button class="ws-button-busy" onclick="wmctrl -s ' %}
{% assign close = '</button>' %}
{% assign unoccupied = '<button class="ws-button" onclick="wmctrl -s ' %}

{{'<box orientation="h" class="workspaces" space-evenly="true">'}}
{% for tag in workspace.tags %}
{% if tag.mine %}
{{mine_open}}{{tag.index | append: '">'}} {{ tag.name }} {{close}}
{% elsif tag.visible  %}
{{visible_open}}{{tag.index | append: '">'}} {{ tag.name }} {{close}}
{% elsif tag.busy  %}
{{busy_open}}{{tag.index | append: '">'}} {{ tag.name }} {{close}}
{% else tag.visible  %}
{{unoccupied}}{{tag.index | append: '">'}} {{ "·" }} {{close}}
{% endif %}
{% endfor %}
{{"</box>"}}
```
And these snippets go into your `eww.xml`:
```xml
  <definitions>
    ...
    <def name="bar">
      <box orientation="h" hexpand="true">
        <workspaces />
        <!-- replace the default 'music' widget with our 'workspace-window' -->
        <workspace-window />
        <sidestuff />
      </box>
    </def>
    <def name="workspaces">
      <box orientation="h" class="workspaces" space-evenly="true" halign="center" valign="center">
        <literal content='{{wm-tags}}' />
      </box>
    </def>
    </def> <def name="workspace-window">
      <!-- We use 'class="music"' here to make the snippet instant compatible with the `eww.scss` in the example bar -->
      <box orientation="h" class="music" halign="start" space-evenly="false">
        <box></box>
        <box>{{workspace-window}}</box> 
      </box>
    </def>
    ...
  </definitions>
```
It is important to know at this point that the `<literal>` tag can only take one element in its `content` parameter. If you need to use multiple element you need to put a `<box>` around them, which in this case is already done by the `template.liquid`.
```xml
  <variables>
    ...
    <!-- Script-variables that don't specify an update interval use the tail of the scripts stdout -->
    <script-var name="wm-tags">~/.config/eww/scripts/getleftwmstate</script-var>
    <script-var name="workspace-window" interval="5s">leftwm-state -w 0 -q -s "{{ window_title }}"</script-var>
    ...
  </variables>
```
The `getleftwmstate` script is just a one line shell script:
```shell
#!/bin/bash
leftwm-state -w 0 -t ~/.config/leftwm/themes/current/template.liquid
```
As the `script-var` calls this script without specifying an `interval` eww will grab the tail of the scripts standard output and update the variable every time there is a change.
For demonstration purpose in the `workspace-window` variable we use the `-q` switch so we get only a single output of `leftwm-state` and update with an interval of 5s. In reallity of course grabbing the tail here as well would make much more sense of course.

## Lemonbar
Lemonbar handles things a bit differently, as it doesn't execute the `leftwm-state` command itself, but starts an instance for each workspace in the `up` script and pipes through the standad output to `lemonbar`.
The formatting is quite simple and well described in `man lemonbar`.

## `sizes.liquid`
This also a very common template in leftwm themes has basically the purpose of generating support for multiple side-by-side workspaces on a single screen.
It generates the size properties for bars based on the workspace properties configured in `config.toml` (usually workspace width and starting coordinates) and explicitly set values (usually bar height).

---
For furhter information about `liquid` syntax you can find a comprehensive documentation on https://github.com/Shopify/liquid/wiki/Liquid-for-Designers.
