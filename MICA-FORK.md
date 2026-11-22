# Chromium Mica fork

The `mica-titlebar` branch restores `chrome://flags/#windows11-mica-titlebar`.
Enable the flag and relaunch Chromium. Mica is opt-in and uses the Windows
system titlebar on eligible windows with the system theme. It requires
Windows 11 22H2 or later. High contrast and titlebar accent colors use
Chromium's existing frame rendering.

## Update the fork

Run these commands from this repository with a clean working tree:

```powershell
git switch mica-titlebar
git fetch upstream
git rebase upstream/main
```

If a rebase conflicts, review Windows frame and color changes before
continuing. To abandon an in-progress rebase, run `git rebase --abort`.

The Git repository is a shallow partial clone with sparse checkout enabled.
The `upstream` remote points to Chromium's canonical Git repository. For
a build, expand the working tree with `git sparse-checkout disable`, then
use Chromium's [Windows build instructions](https://chromium.googlesource.com/chromium/src/+/main/docs/windows_build_instructions.md)
to configure depot_tools and sync DEPS for this checkout. Git may download
additional objects from upstream when expanding the working tree.

After a Windows build, verify the flag appears, takes effect after relaunch,
and can be disabled again. Check light and dark themes, native caption
buttons, maximized and restored windows, and horizontal and vertical tabs.

The implementation is based on the code removed in upstream commit
[`597e54a1b91a`](https://chromium.googlesource.com/chromium/src/+/597e54a1b91a5eac141894651f7ed3671ab33a17).
