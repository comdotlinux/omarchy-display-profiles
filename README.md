# Display Profiles — Omarchy plugin

Extends the Omarchy **Display** bar panel (built-in `omarchy.monitor`) with a
**DISPLAY PROFILES** section: buttons for each saved
`~/.config/nwg-displays/profiles/*.json`, the active one highlighted. Click one
to apply it via `nwg-displays-apply -p <name>` — the same headless apply
Displays Settings uses: it rewrites `hypr/monitors.conf` + `hypr/monitors.lua`
and reloads Hyprland.

Everything else in the Display panel (brightness, text size, scale, displays)
is the stock built-in panel this plugin forks.

## Install

```bash
omarchy plugin add https://github.com/comdotlinux/omarchy-display-profiles.git --enable
```

Then put it in the bar in place of the built-in Display widget — either keep
both buttons and just add this one

```bash
omarchy bar move comdotlinux.display-profiles --section right
```

or edit `~/.config/omarchy/shell.json` and replace the `omarchy.monitor`
entry with `comdotlinux.display-profiles`.

**Requirements:** `nwg-displays` (with `nwg-displays-apply`) and `jq` — both
ship with Omarchy. If `nwg-displays` is missing, the section shows a
`sudo pacman -S nwg-displays` hint instead of profile buttons.

## Keybind (optional)

In `hypr/bindings.lua`:

```lua
o.bind("SUPER + SHIFT + CTRL + M", "Display profiles", "omarchy-shell shell toggle comdotlinux.display-profiles '{}'")
```

## Notes

- Per-profile workspace rules stay user-side (in `hypr/workspaces.lua`, keyed
  on `~/.config/nwg-displays/active_profile.json`); the plugin does not manage them.
- The panel keeps the built-in's IPC target (`omarchy.monitor`), so existing
  keybinds/scripts keep working.
- Profiles are created in Displays Settings (nwg-displays) → Apply a layout →
  Profile → save; new profiles appear in the panel automatically.

## Remove

```bash
omarchy plugin remove comdotlinux.display-profiles
```

(restore the built-in widget in the bar afterwards, if you replaced it)

## License

MIT — includes code derived from Omarchy's built-in `omarchy.monitor`
panel (MIT, © the Omarchy authors).
