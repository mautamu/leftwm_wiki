This is a brief overview of the available external commands and their possible arguments.

Generally you pass the string of the external command to `$XDG_RUNTIME_DIR/leftwm/command.pipe`.
For example from a shell you could use:
```shell
echo "SetLayout CenterMain" > $XDG_RUNTIME_DIR/leftwm/command.pipe
```
|Command | Arguments (if needed) | Notes |
|-|-|-|
| Reload | | Reloads leftwm |
| LoadTheme | `Path-to/theme.toml` | usually used in themes `up` script to load a theme |
| UnloadTheme | | usually used in themes `down` script to unload the theme |
| SetLayout | `LayoutName` | |
| NextLayout | | |
| PreviousLayout | | |
| RotateTag | | |
| SetMarginMultiplier | `multiplier as float` | set a factor by which the margin gets mutliplied, use "1.0" to reset, negative values will be abs-converted |
| SwapScreen | | swaps two screens/workspaces |
| SendWorkspaceToTag | `workspace index` `tag_index` | both indizes as integer, focuses `Tag` on `Workspace` |
| SendWindowToTag | `tag_index` | index as integer, sends currently focused window to `Tag` |
| MoveWindowToLastWorkspace | | moves currently focused window to last used workspace |
| MoveWindowDown | | moves currently focused window down once |
| MoveWindowUp | | moves currently focused window up once |
| MoveWindowTop | | moves currently focused window to the top |
| FloaingToTile | | pushes currently focused floating window back to tiling mode |
| CloseWindow | | closes currently focused window |
| FocusWindowDown | | |
| FocusWindowU | | |
| FocusNextTag | | |
| FocusPreviousTag | | |
| FocusWorkspaceNext | | |
| FocusWorkspacePrevious | | |
